# DNS INstallation and Configuration

### Instalation
```sh
#yum install bind
```

### Configuration
add this script 

```sh
zone "pon-peparnas2016jabar.go.id" IN {
type master;
file "pon-peparnas2016jabar.go.id";
allow-update { none; };
};
```
add to /etc/named.conf

```sh
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

options {
	listen-on port 53 { 127.0.0.1;10.200.0.10; };
	listen-on-v6 port 53 { ::1; };
	directory 	"/var/named";
	dump-file 	"/var/named/data/cache_dump.db";
	statistics-file "/var/named/data/named_stats.txt";
	memstatistics-file "/var/named/data/named_mem_stats.txt";
	allow-query     { localhost; 10.200.0.0/24;};

	/* 
	 - If you are building an AUTHORITATIVE DNS server, do NOT enable recursion.
	 - If you are building a RECURSIVE (caching) DNS server, you need to enable 
	   recursion. 
	 - If your recursive DNS server has a public IP address, you MUST enable access 
	   control to limit queries to your legitimate users. Failing to do so will
	   cause your server to become part of large scale DNS amplification 
	   attacks. Implementing BCP38 within your network would greatly
	   reduce such attack surface 
	*/
	recursion yes;

	dnssec-enable yes;
	dnssec-validation yes;
	dnssec-lookaside auto;

	/* Path to ISC DLV key */
	bindkeys-file "/etc/named.iscdlv.key";

	managed-keys-directory "/var/named/dynamic";

	pid-file "/run/named/named.pid";
	session-keyfile "/run/named/session.key";
};

logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};

zone "pon-peparnas2016jabar.go.id" IN {
type master;
file "pon-peparnas2016jabar.go.id";
allow-update { none; };
};

zone "." IN {
	type hint;
	file "named.ca";
};

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";


```

create file /var/named/pon-peparnas2016jabar.go.id

```sh
$TTL 86400
@   IN  SOA     masterdns.pon-peparnas2016jabar.go.id. root.pon-peparnas2016jabar.go.id. (
        2011071001  ;Serial
        3600        ;Refresh
        1800        ;Retry
        604800      ;Expire
        86400       ;Minimum TTL
)
@       IN  NS          masterdns.pon-peparnas2016jabar.go.id.
@       IN  NS          secondarydns.pon-peparnas2016jabar.go.id.
@       IN  A           10.200.0.11
@       IN  A           10.200.0.11
@       IN  A           10.200.0.11
masterdns       IN  A   10.200.0.11
secondarydns    IN  A   10.200.0.11
client          IN  A   10.200.0.11

```

#### Firewall
```sh
Check your firewall
# systemctl status firewalld
# firewall-cmd --state
# firewall-cmd --zone=public --list-all
# firewall-cmd --list-services
# cat /etc/firewalld/zones/public.xml
Open port 25 and 2053 and other services
# firewall-cmd --permanent --zone=public --add-service=dns
Reload all setting using –permanent option only
# firewall-cmd --reload
Remove port access
# firewall-cmd --permanent --zone=public –-remove-port=443/tcp
# firewall-cmd --zone=public --remove-port=80/tcp --permanent
# firewall-cmd --zone=public --remove-port=7071/tcp
``` 
Note: The previous command displays the current configuration, ie the permanent settings and the temporary ones. To only get the permanent settings, use the –permanent option.


### Starting Service

```sh
#systemctl restart named
```
