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

    ![image](https://github.com/joinia/webray.com.cn/blob/main/Bludit/images/add.png)

4. Use "burp"  to capture and change packages

   ![image](https://github.com/joinia/webray.com.cn/blob/main/Bludit/images/package-1.png)

   ![image](https://github.com/joinia/webray.com.cn/blob/main/Bludit/images/package-2.png)

5. Viewing the successfully published page,We can see the alert.

   ![image](https://github.com/joinia/webray.com.cn/blob/main/Bludit/images/finish.png)
 
   ![image](https://github.com/joinia/webray.com.cn/blob/main/Bludit/images/alert.png)
