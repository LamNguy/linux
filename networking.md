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
 
 [link_create_vpn_tunnel_namespace](https://howto.lintel.in/run-openvpn-tunnel-inside-network-namespace/)
 
 
 
 ***Link local*** \
 [Link](https://en.wikipedia.org/wiki/Link-local_address) \
 Network 169.254.0.0/16 cho phép các máy trong subnet giao tiếp với nhau ( không giám sát việc trùng địa chỉ ip ) , khi dhcp gặp sự cố không hoạt động được hoặc không có ip tĩnh thì máy tính sẽ dùng dải địa chỉ này 
-- See more in Zero Configuation Networking \
-- avahi-autoipd \ 
-- avahi-autoipd sẽ check xem có địa chỉ ip nào sẵn có không , nếu có thì nó sẽ không tự gán zero-config nữa , sử dụng avahi-autoipd --force-bind để tự  động gán địa chỉ 169.254 kể cả  khi có địa chỉ ip sẵn có . 


***Bridge Networking***\
`yum install bridge-utils`  \
`man brctl 

Check các port đang listnening `netstat -nlpt`






