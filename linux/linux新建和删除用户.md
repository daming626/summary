
#创建用户

1、useradd username

2、useradd -m -d /home/username -s /bin/bash username

#删除用户

1、userdel -r username  将用户和用户组全部删除

2、userdel username 只删除用户，用户组信息残留，无法再创建同名用户

#删除由userdel username 残留的用户组信息

1、删除 /home 目录下的文件

- rm -rf name

2、删除 /etc/passwd 下的用户信息

- vi /etc/passwd 

3、删除 /etc/group 下的用户组文件

- vi /etc/group

4、删除 /var/spool/mail 下的邮箱文件

- rm -rf name

5、如果/home下的username无法删除，使用以下其中一个删除

- find / -nouser -o -nogroup -exec rm -rf {} \;
- find / -nouser -o -nogroup |xargs  rm -rf {}