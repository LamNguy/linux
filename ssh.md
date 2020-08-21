In some case , password authentication will be disable by default \
To enable ssh ***password authentication*** , edit file :\
`/etc/ssh/sshd_config` \
and change the line : \
`PasswordAuthentication no` \
to \
`PasswordAuthentication yes`


To enable ***Root login*** , edit file :\
`/etc/ssh/sshd_config` \
and change the line : \
`PermitRootLogin no`\
to \
`PermitRootLogin yes`\
and restart ssh service : `sudo service ssh restart` and not forget to set root password : `sudo passwd root`
