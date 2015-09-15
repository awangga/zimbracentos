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
to use smtp relay server
# zmprov mcf zimbraMtaRelayHost smtp.telkom.net:587
and edit global config on web admin port 7071
# zmprov getAllConfig | grep zimbraMtaSmtpdClientRestrictions
for looking smtpd_client_restrictions variable
# zmprov mcf zimbraMtaSmtpdClientRestrictions permit_sasl_authenticated
changing smtpd_client_restrictions variable from default reject_unauth_pipelining to permit_sasl_authenticated
# zmprov mcf zimbraMtaSmtpdClientRestrictions permit_sasl_authenticated,permit_mynetworks,reject_unauth_pipelining
change mode to alwasy https
# zmtlsctl redirect
change admin port, zimbraAdminPort can change with other param
# zmprov ms mail.unm.ac.id zimbraAdminPort 1213
```


### Starting Service
Make sure no postfix running : service postfix stop
```sh
#su -zimbra
$zmcontrol start
$zmcontrol status
```
Admin Panel on locahost:7071 for client on port 80


### Uninstall ZImbra
```sh
# su – zimbra
$ zmcontrol stop
$ exit
# ps -ef | grep -i zimbra
# kill -9 <pid>
# df
# umount /opt/zimbra/amavisd<-new-blah>/tmp
# cd /<tmp_tar_install_dir>/zcs/
# ./install.sh -u
# rm -rf /opt/zimbra
# rm -rf /var/log/*zimbra*
# rm -rf /tmp/*zimbra*
# rm -rf /tmp/hsperfdata*
# rm -rf /tmp/install.*
# rm -rf /tmp/*swatch*
# rm -rf /tmp/log*
# userdel zimbra
# userdel postfix
# groupdel zimbra
# groupdel postfix
# systemctl stop zimbra
# systemctl disable zimbra
```


### Referensi
 1. http://cloudindonesia.com/tutorial-instalasi-zimbra-di-centos-6-5/
 2. http://wiki.zimbra.com/wiki/CentOS_6.3_and_Zimbra_8_Install_Guide
 3. https://wiki.zimbra.com/wiki/UnInstalling_Zimbra_on_Linux
 4. https://wiki.zimbra.com/wiki/CLI_zmtlsctl_to_set_Web_Server_Mode