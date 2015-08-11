# zimbracentos
Zimbra on Centos

### Pra instalasi
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

### Referensi
 1. http://cloudindonesia.com/tutorial-instalasi-zimbra-di-centos-6-5/
 2. http://wiki.zimbra.com/wiki/CentOS_6.3_and_Zimbra_8_Install_Guide