***1.Disable IPv6 ( no reboot required )***

Verify IPv6 : `# ifconfig -a | grep inet6`

Append below lines in /etc/sysctl.conf:

`net.ipv6.conf.all.disable_ipv6 = 1`

`net.ipv6.conf.default.disable_ipv6 = 1`

NOTE : To disable IPv6 on a single interface add below lines to /etc/sysctl.conf :
net.ipv6.conf.[interface].disable_ipv6 = 1 ### put interface name here [interface]
net.ipv6.conf.default.disable_ipv6 = 1


 To make the settings affective, execute :\
 `# sysctl -p`
 
 NOTE : make sure the file /etc/ssh/sshd_config contains the line AddressFamily inet to avoid breaking SSH Xforwarding if you are using the sysctl method
 
 ` systemctl restart sshd `
 
 ***Network namespace***
 
