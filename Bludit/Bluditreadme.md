# Bludit Authenticated Stored Cross-Site Scripting(XSS)

#### Description

Persistent XSS (or Stored XSS) attack is one of the three major categories of XSS attacks, the others being Non-Persistent (or Reflected) XSS and DOM-based XSS. In general, XSS attacks are based on the victim’s trust in a legitimate, but vulnerable, website or web application.Bludit CMS does not filter the content correctly at the "new content" module, resulting in the generation of stored XSS.

#### Affects CMS

Bludit CMS v3.13.1

https://www.bludit.com/

#### Author

webraybtl@webray.com.cn inc

#### Proof of Concept

1. Login the CMS.

2. Open Page http://127.0.0.1:8086/admin/new-content

3. Put XSS payload  (<script>alert(1)</script>) in the content box and click on save to publish the page

   <img src="D:\cves\Bludit\images\add.png" alt="add" style="zoom: 33%;" />

4. Use "burp"  to capture and change packages

   ![package-1](D:\cves\Bludit\images\package-1.png)

   ![package-2](D:\cves\Bludit\images\package-2.png)

5. Viewing the successfully published page,We can see the alert.



 ![finish](D:\cves\Bludit\images\finish.png)

![alert](D:\cves\Bludit\images\alert.png)
