# Lab Inconsistent handling of exceptional input

This lab doesn't adequately validate user input. You can exploit a logic flaw in its account registration process to gain access to administrative functionality. To solve the lab, access the admin panel and delete Carlos.

Lesson Learned: Try unexpected inputs that the developers may not have expected and accounted for. In this lab, the developer failed to properly handle extra long email addresses which resulted in me being able to register and receive an email confirmation to an address that I (somewhat) did not own.

-----------------------------------------------------------
This is what the landing page looks like

![[Pasted image 20211003133121.png]]

From my email account, it looks like I will receive any emails and subdomains for the highlighted domain

![[Pasted image 20211004014758.png]]

To complete this lab, I need to register with the @dontwannacry email address. 

I tried registering with the following email address

 hacker@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net


![[Pasted image 20211004014905.png]]

After registering, I received the following verification link

![[Pasted image 20211004014933.png]]


After logging in, I can see my email.

![[Pasted image 20211004014957.png]]

Unfortunately, I cannot access the admin panel, despite having "dontwannacry" in my email address.

![[Pasted image 20211004015045.png]]

I tried a couple things, like registering with capitolizations, null bytes at the end of the email.

We need to figure out how to drop the "exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net" section of my email which would allow my email client to still have the verification code and have my email set to "dontwannacry" only. 

After a couple of hours, I ended up looking at the answer.

The issue in this program cannot properly handle large email arguments. If I enter a long email address, then when the program reaches its capacity, then it will cut off the end of the email address 

This would allow me to have an email address of @dontwannacry.com instead of @dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net

I registered with the following account


hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net


![[Pasted image 20211004015958.png]]

After logging in with this registered account, the exploit domain did not get dropped

![[Pasted image 20211004020156.png]]

I will try registering with an EVEN longer email address

hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net

After logging in, we can see that too much of the email was dropped

![[Pasted image 20211004020341.png]]

Registering with the following email address should get what we want.

hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net


![[Pasted image 20211004020502.png]]

After logging in, this is the result. Sooo close!

![[Pasted image 20211004020613.png]]

I subtracted one of the "a" characters, which should allow me to have "dontwannacry.com" in my email.

I registered 

hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net

![[Pasted image 20211004020736.png]]

After logging in, we have the email domain of just "@dontwannacry.com"

![[Pasted image 20211004020831.png]]

Now when I can successfully visit /admin 

![[Pasted image 20211004020856.png]]

Nice!

![[Pasted image 20211004020913.png]]