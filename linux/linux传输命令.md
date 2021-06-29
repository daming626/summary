### secureCRT传文件

alt p 进入sftp模式

- put filepath 上传文件 
- get filepath 下载文件

### flashFXP传文件

- yum install vsftpd  

- ps -ef|grep vsftpd        查看ftp端口？（kill 端口号）

- which vsftpd       查看vsftpd地址

- ./vsftpd        启动vsftpd

- 以上启动后在flashFXP中新建一个站点输入（1、地址 2、服务器中的用户名，非根用户root 3、服务器密码）

  