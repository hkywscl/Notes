### 基于Ubuntu系统的Apache服务器的多站点配置

#### 1.修改文件/etc/apache2/sites-available/000-default.conf(相当于windows系统本机wamp\bin\apache\apache2.4.18\conf\extra\httpd-vhosts.conf)，设置不同的ServerName、DocumentRoot 和 Directory 

```
<VirtualHost *:8080>
   ServerAdmin webmaster1@localhost
   DocumentRoot 项目路径1
   ServerName www.aaa.com

   <Directory 项目路径1>
   Options Indexes FollowSymLinks
   AllowOverride All
   Require all granted
   </Directory>

   ErrorLog ${APACHE_LOG_DIR}/error.log
   CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

<VirtualHost *:8081>
   ServerAdmin webmaster1@localhost
   DocumentRoot 项目路径2
   ServerName www.bbb.com

   <Directory 项目路径2>
   Options Indexes FollowSymLinks
   AllowOverride All
   Require all granted
   </Directory>

   ErrorLog ${APACHE_LOG_DIR}/error.log
   CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```



#### 2.更新Apache监听端口： 编辑 /etc/apache2/ports.conf 文件，添加以下内容：
```
Listen 8080
Listen 8081
```



#### 3.重启apache，`systemctl restart apache2`



#### 4.完成
