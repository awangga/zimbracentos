# zimbracentos
Zimbra on Centos

## Centos 6

### Pra instalation
```sh
# vi /etc/sysconfig/network
HOSTNAME=dev.jabar2016.com
# vi /etc/hosts
103.30.244.230 dev.jabar2016.com dev
```

```sh
#yum install system-config-network-tui system-config-firewall-tui nc sudo mysql mysql-server mysql-devel sysstat wget bind bind-utils –y
#wget http://files2.zimbra.com/downloads/8.0.6_GA/zcs-8.0.6_GA_5922.RHEL6_64.20131203103705.tgz
#tar –xzvf zcs-8.0.6_GA_5922.RHEL6_64.20131203103705.tgz 
#cd zcs-8.0.6_GA_5922.RHEL6_64.20131203103705
#./install.sh --platform-override
```
Config please set admin password

### Starting Service
Make sure no postfix running : service postfix stop
```sh
#su -zimbra
$zmcontrol start
$zmcontrol status
```
Admin Panel on locahost:7071 for client on port 80

## Centos 7

### Pra instalation
```sh
# vi /etc/hostname 
dev.jabar2016.com
# vi /etc/hosts
103.30.244.230 dev.jabar2016.com dev
```

### Instalation
```sh
#yum install system-config-network-tui system-config-firewall-tui nc sudo mysql mysql-server mysql-devel sysstat wget bind bind-utils –y
#wget https://files.zimbra.com/downloads/8.6.0_GA/zcs-8.6.0_GA_1153.RHEL7_64.20141215151110.tgz
#tar –xzvf zcs-8.6.0_GA_1153.RHEL7_64.20141215151110.tgz
#cd zcs-8.6.0_GA_1153.RHEL7_64.20141215151110
#./install.sh --platform-override
```

### Configuration
please set admin password. to reconfig please run :
```sh
# /opt/zimbra/libexec/zmsetup.pl
to change password
# su - zimbra
# zmprov sp <user or admin email address> <new password>
```


### Starting Service
Make sure no postfix running : service postfix stop
```sh
#su -zimbra
$zmcontrol start
$zmcontrol status
```
Admin Panel on locahost:7071 for client on port 80

### Referensi
 1. http://cloudindonesia.com/tutorial-instalasi-zimbra-di-centos-6-5/
 2. http://wiki.zimbra.com/wiki/CentOS_6.3_and_Zimbra_8_Install_Guide