# Lab Inconsistent security controls

## Objective: 

This lab's flawed logic allows arbitrary users to access administrative functionality that should only be available to company employees. To solve the lab, access the admin panel and delete Carlos.

## Big Idea"

Applications may appear to be secure because they implement seemingly robust measures to enforce the business rules. Unfortunately, some applications make the mistake of assuming that, having passed these strict controls initially, the user and their data can be trusted indefinitely. This can result in relatively lax enforcement of the same controls from that point on.

If business rules and security measures are not applied consistently throughout the application, this can lead to potentially dangerous loopholes that may be exploited by an attacker.

--------------------------------------------


This is what the register account page looks like

![[Pasted image 20211004021850.png]]

I do not have control of the "dontwannacry" email domain, but I do have control of the exploit-ac7a1f3d1fe06918809008cc018100fb.web-security-academy.net domain.

I started by registering with the following account.

![[Pasted image 20211004022005.png]]

From my email client, I received a verification link

![[Pasted image 20211004022048.png]]

After I verified my account, I was able to login with the registered account

![[Pasted image 20211004022154.png]]

After logging in, I was welcomed by the following page.

![[Pasted image 20211004022232.png]]

I visited /admin to see if I had access. Unfortunately, I did not have access because I do not have a dontwannacry email address

![[Pasted image 20211004022347.png]]

I will try changing my email address to hacker@dontwannacry.com

![[Pasted image 20211004022518.png]]

![[Pasted image 20211004022527.png]]

Now, that I changed my email, I was able to visit the /admin page 

![[Pasted image 20211004022549.png]]

![[Pasted image 20211004022606.png]]