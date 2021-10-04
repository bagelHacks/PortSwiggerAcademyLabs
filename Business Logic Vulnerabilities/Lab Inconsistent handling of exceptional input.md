# Lab Inconsistent handling of exceptional input

This lab doesn't adequately validate user input. You can exploit a logic flaw in its account registration process to gain access to administrative functionality. To solve the lab, access the admin panel and delete Carlos.

Lesson Learned: Try unexpected inputs that the developers may not have expected and accounted for. In this lab, the developer failed to properly handle extra long email addresses which resulted in me being able to register and receive an email confirmation to an address that I (somewhat) did not own.

-----------------------------------------------------------
This is what the landing page looks like

![image](https://user-images.githubusercontent.com/90155329/135806266-9fa9cd82-2350-4af1-96bb-a19eed58a624.png)

From my email account, it looks like I will receive any emails and subdomains for the highlighted domain

![image](https://user-images.githubusercontent.com/90155329/135806283-86466f56-5d3e-4b3b-a146-b613396fb3e1.png)

To complete this lab, I need to register with the @dontwannacry email address. 

I tried registering with the following email address

 hacker@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net


![image](https://user-images.githubusercontent.com/90155329/135806301-6ab10afa-539c-4e35-9e5a-6bc04471360e.png)

After registering, I received the following verification link

![image](https://user-images.githubusercontent.com/90155329/135806323-50c6d2e7-1120-4e60-a3c2-8c7e6d28f6bd.png)


After logging in, I can see my email.

![image](https://user-images.githubusercontent.com/90155329/135806340-6ff5e3db-aa5a-4b87-8f64-95b26ed429b5.png)

Unfortunately, I cannot access the admin panel, despite having "dontwannacry" in my email address.

![image](https://user-images.githubusercontent.com/90155329/135806373-4b8c219d-0294-4fd4-84c8-376bf6353a00.png)

I tried a couple things, like registering with capitolizations, null bytes at the end of the email.

We need to figure out how to drop the "exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net" section of my email which would allow my email client to still have the verification code and have my email set to "dontwannacry" only. 

After a couple of hours, I ended up looking at the answer.

The issue in this program cannot properly handle large email arguments. If I enter a long email address, then when the program reaches its capacity, then it will cut off the end of the email address 

This would allow me to have an email address of @dontwannacry.com instead of @dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net

I registered with the following account


hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net


![image](https://user-images.githubusercontent.com/90155329/135806404-48b3967f-ccce-4359-a4ca-98c14518a4ca.png)

After logging in with this registered account, the exploit domain did not get dropped

![image](https://user-images.githubusercontent.com/90155329/135806436-8e2ea212-43ca-457f-a94c-30ab30c1d973.png)

I will try registering with an EVEN longer email address

hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net

After logging in, we can see that too much of the email was dropped

![image](https://user-images.githubusercontent.com/90155329/135806459-f97ee63e-b9e7-4a56-945e-2d3430bfe3dc.png)

Registering with the following email address should get what we want.

hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net


![image](https://user-images.githubusercontent.com/90155329/135806527-27ddfdfb-16ca-4aaa-a1c1-435e4435da26.png)

After logging in, this is the result. Sooo close!

![image](https://user-images.githubusercontent.com/90155329/135806720-dbe6d52b-a7d3-4e58-a5e0-cf1dd4f717c3.png)

I subtracted one of the "a" characters, which should allow me to have "dontwannacry.com" in my email.

I registered 

hackeraaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@dontwannacry.com.exploit-ac411f011e8c523980eb0e47010300d4.web-security-academy.net

![image](https://user-images.githubusercontent.com/90155329/135806753-4676f257-ae28-4d9f-81e3-d3904637c924.png)

After logging in, we have the email domain of just "@dontwannacry.com"

![image](https://user-images.githubusercontent.com/90155329/135806785-1683b753-2169-4499-99b9-38ffeb86036b.png)

Now when I can successfully visit /admin 

![image](https://user-images.githubusercontent.com/90155329/135806830-a60c066b-c771-4b6f-85a1-c327dab0dc56.png)

Nice!

![image](https://user-images.githubusercontent.com/90155329/135806857-b97f2297-5535-4d08-8427-305a8f5e6740.png)
