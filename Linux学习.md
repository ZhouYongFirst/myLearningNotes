## 1. sendmail安装及配置
（1）检查是否安装了sendmail：
```
rpm -qa | grep sendmail
```

（2）若已安装，执行下一步；若未安装，则：
```
yum install sendmail
```

（3）修改配置文件：
```
vim /etc/mail/sendmail.mc    //修改sendmail配置文件模板
```
将```DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl```中的127.0.0.1改为0.0.0.0意思是任何主机都可以访问sendmail服务。

（4）生成配置文件：
```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```
若系统无法识别m4命令，安装sendmail-cf软件包：`yum install sendmail-cf`;
生成配置文件前可以对原配置文件做备份：`mv sendmail.cf sendmail.cf.old`。

（5）启动sendmail服务：
```
systemctl start sendmail.service
```

（6）测试邮件能否正常发送：
```
echo "testmail" | mail -s "test" test@example.com   //test为邮件主题，test@example.com为收件人邮箱，前面的为邮件内容
```

<font color="#cc0000">注意事项:</font>   
腾讯云或阿里云服务器的25号端口默认被封禁，导致无法正常发送邮件，需要去官网解封。

使用外部smtp服务器发送邮件：
- 修改文件/etc/mail.rc:
```
vim /etc/mail.rc
```
设置如下：
```
set from=test@example.com
set smtp=smtp.example.com
set smtp-auth-user=username
set smtp-auth-password=password
set smtp-auth=login
```
from表示发送的邮件地址；  
smtp是外部smtp服务器的地址；  
smtp-auth-user是外部smtp服务器认证的用户名（邮箱账号）；  
smtp-auth-password是外部smtp服务器的客户端授权码；  
smtp-auth是邮件认证方式。
