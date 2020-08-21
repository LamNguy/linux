In some case , password authentication will be disable by default \
***1.To enable ssh password authentication***\
edit file : `/etc/ssh/sshd_config` \
and change the line : \
`PasswordAuthentication no` \
to \
`PasswordAuthentication yes`


***2.To enable Root login***\
edit file :`/etc/ssh/sshd_config`\
and change the line : \
`PermitRootLogin no`\
to \
`PermitRootLogin yes`\
and restart ssh service : `sudo service ssh restart` and not forget to set root password : `sudo passwd root`


***3.Restrict certain user log onto a system via ssh server***

`AllowUsers user1 user2`

AllowUsers keyword can be followed by a list of user  name patterns , seperated by space . If it specified ,login is only allowed for user names that match one of the pattern ,. * and ?  can be used as wildcards in the patterns . By default , all users are allowed. 

`# vi /etc/ssh/sshd_config`

`# /etc/init.d/sshd restart`

***4.File transfer remotely via ssh using scp***

  Copy single file from local to remote: \
  `$ scp myfile.txt remoteuser@remoteserver:/remote/folder/` 

  Copy singe file from remote to local: \
  `$ scp remoteuser@remoteserver:/remote/folder/myfile.txt  myfile.txt`
  
  Copy mutilple files from local to remote: \
  `$ scp myfile.txt myfile2.txt remoteuser@remoteserver:/remote/folder/`
  
  Copy all files from local to remote :\
  `$ scp * remoteuser@remoteserver:/remote/folder/`
  
  Copy all files and folders recursively from local to remote : \
  `$ scp myfile.txt myfile2.txt remoteuser@remoteserver:/remote/folder/`
