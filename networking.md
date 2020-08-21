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
 So what are network namespaces? Generally speaking, an installation of Linux shares a single set of network interfaces and routing table entries. You can modify the routing table entries using policy routing , but that doesn’t fundamentally change the fact that the set of network interfaces and routing tables/entries are shared across the entire OS. Network namespaces change that fundamental assumption. With network namespaces, you can have different and separate instances of network interfaces and routing tables that operate independent of each other.
 
 - Create network namespace \
 `ip netns add namespace`
  
 to assign a physical interface to a network namespace, you’d use this command \
 `ip link set dev <device> netns <namespace> ?? ` 
 
 ` ip link `
 
 ` ip addr`
 
 ` ip route `
 
 : A reader contacted me to point out that it’s possible to create the veth pairs and assign one of the pairs to a network namespace all in one command:
 
 
 ` ip link add veth0 type veth peer name veth1 netns blue`
  
 
 Connect network namespace to the Physical Network : just use a bridge 
 
 
 
 
 
