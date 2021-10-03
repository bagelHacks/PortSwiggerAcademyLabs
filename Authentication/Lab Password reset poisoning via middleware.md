# Lab Password reset poisoning via middleware


Objective: 

This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any links in emails that he receives. To solve the lab, log in to Carlos's account. You can log in to your own account using the following credentials: wiener:peter. Any emails sent to this account can be read via the email client on the exploit server. 

I will start by logging into wiener's account. This simulates an account that we have control oveer

Start by resetting wiener's account

![image](https://user-images.githubusercontent.com/90155329/134100392-e8433219-beb2-47bd-baef-da9102e3370f.png)

This sent me the following link

![image](https://user-images.githubusercontent.com/90155329/134100408-5881846c-012a-4d11-b884-f7c9e9a3b7fb.png)

https://ac9b1fee1e8e665880e516f9003c0058.web-security-academy.net/forgot-password?temp-forgot-password-token=xmOb90CgmcURcYvg7OnSUrp5abyJENtY

I followed the link to the following password reset page:

![image](https://user-images.githubusercontent.com/90155329/134100426-584360b3-52fe-44c7-8e2e-6a64045830ae.png)

Lets see what the request looks like when I reset the wiener user:

![image](https://user-images.githubusercontent.com/90155329/134100434-5e0409c1-e7b1-4066-95b1-154343ae3a85.png)

![image](https://user-images.githubusercontent.com/90155329/134100442-1fd08162-ad3d-41a3-9087-f4ea64beae5e.png)

Now that I understand what a reset looks like, it would be very interesting to get Carlos's token. If I can get a reset token from Carlos's I can visit the password reset page and reset his account. 

The "X-Forward-Host" is a header used by proxies to know where to send client requests too. 

In this case, if I attempt to reset carlos's account and I can add the x-forwarded-host header with the location of my exploit server, then when the server responds with the special password reset token of carlos's account, a copy will get sent to my exploit server.

First get the domain of my exploit server (that comes with Portswigger Labs)


 https://exploit-ac961fe91fc0608480697381015400a6.web-security-academy.net/exploit
 
 ![image](https://user-images.githubusercontent.com/90155329/134100467-6537d55f-853e-4833-9f03-d21c530b665f.png)


exploit-ac961fe91fc0608480697381015400a6.web-security-academy.net/exploit

Reset wiener account

![image](https://user-images.githubusercontent.com/90155329/134100482-2cee1272-ee35-4415-853e-35476633eda0.png)

intercept request with burp 

![image](https://user-images.githubusercontent.com/90155329/134100506-7623eaf5-4e5a-420e-8506-797091233563.png)

Add the x-forward-host header with the domain of my exploit server.


![image](https://user-images.githubusercontent.com/90155329/134100514-b50e8e77-2a3d-4561-b517-9651d4d638b5.png)


Since the x-forwarded-host was part of the http header, when carlos received the password reset email and clicks on it, a request to that reset link will be sent to the x-forward-host value. Visiting my web access logs, I can see the request with carlos's token.

172.31.31.96    2021-09-21 01:46:26 +0000 "GET /forgot-password?temp-forgot-password-token=Sxh5lUws9FgWGMULFFBGSEpjMOcoA2SI HTTP/1.1" 404 "User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36"

![image](https://user-images.githubusercontent.com/90155329/134100528-71be84a0-1005-4226-8af4-a26fe2b7d74d.png)

Now when I visit /forgot-password?temp-forgot-password-token=Sxh5lUws9FgWGMULFFBGSEpjMOcoA2SI, I can reset carlos's password

![image](https://user-images.githubusercontent.com/90155329/134100563-3101c1e2-27b8-499c-862e-b4f0ab1cfc77.png)

Now I can login with carlos's credentials.

![image](https://user-images.githubusercontent.com/90155329/134100579-8d1b1a92-f1c2-4385-aed1-2ead66f8e36f.png)

![image](https://user-images.githubusercontent.com/90155329/134100598-f66df8b1-a745-476a-aa33-08a7aaab9a74.png)
