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
  
  **Note** : remote user need have write permission to /remote/folder in the remote system . \
  **Another method transfer** : SFTP ,  RSYNC \
  
 **5.Execute local scripts on remote machine and include arguments** \
 
`$ ssh remote_server "bash -s" < ./file_bash [arguments]`

SSH Config File Location

OpenSSH client-side configuration file is named config, and it is stored in .ssh directory under user’s home directory.
$mkdir -p ~/.ssh && chmod 700 ~/.ssh

The ~/.ssh directory is automatically created when the user runs the ssh command for the first time. If the directory doesn’t exist on your system, create it using the command below:
touch ~/.ssh/config

This file must be readable and writable only by the user, and not accessible by others:
chmod 600 ~/.ssh/config

 The SSH Config File takes the following structure:
 
 Host hostname1
    SSH_OPTION value
    SSH_OPTION value

Host hostname2
    SSH_OPTION value

Host *
    SSH_OPTION value
 
 
* - Matches zero or more characters. For example, Host * matches all hosts, while 192.168.0.* matches hosts in the 192.168.0.0/24 subnet.
? - Matches exactly one character. The pattern, Host 10.10.0.? matches all hosts in 10.10.0.[0-9] range.
! - When used at the start of a pattern, it negates the match. For example, Host 10.10.0.* !10.10.0.5 matches any host in the 10.10.0.0/24 subnet except 10.10.0.5.



Host targaryen
    HostName 192.168.1.10
    User daenerys
    Port 7654
    IdentityFile ~/.ssh/targaryen.key

Host tyrell
    HostName 192.168.10.20

Host martell
    HostName 192.168.10.50

Host *ell
    user oberyn

Host * !martell
    LogLevel INFO

Host *
    User root
    Compression yes
    
    
    
If you want to override a single option, you can specify it on the command line. For example, if you have the following definition:

Host dev
    HostName dev.example.com
    User john
    Port 2322
Copy
and you want to use all other options but to connect as user root instead of john simply specify the user on the command line:

ssh -o "User=root" dev
The -F (configfile) option allows you to specify an alternative per-user configuration file.

To tell the ssh client to ignore all of the options specified in the ssh configuration file, use:
ssh -F /dev/null user@example.com
