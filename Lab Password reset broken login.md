# Lab Password reset broken login

Objective:

 This lab's password reset functionality is vulnerable. To solve the lab, reset Carlos's password then log in and access his "My account" page.

    Your credentials: wiener:peter
    Victim's username: carlos

This lab involves attacking the "Forgot password" functionality

![[Pasted image 20210919175959.png]]

Since, I have credentials to a valid account, I will try resetting their password. Analyzing this process may uncover how this functionality can be attacked.

![[Pasted image 20210919180138.png]]

Submitting this password reset request sent a password reset link the wiener's email

![[Pasted image 20210919180226.png]]

This is the password reset link that was provided.

https://acb01f361fcff14380240af3005a002c.web-security-academy.net/forgot-password?temp-forgot-password-token=nYOjWrnhOylN1M8GFiLvZ1kexY0ap3Ad

The link brought me to a password reset page:

![[Pasted image 20210919180849.png]]

The base64 value of nYOjWrnhOylN1M8GFiLvZ1kexY0ap3Ad looks interesting.

I wonder if I can reset a password by deleting the token value 

I tried to reset the password, and intercepted the post request

![[Pasted image 20210919181039.png]]

![[Pasted image 20210919181047.png]]

This is interesting. I wonder, if I I can modify the username value to change the value of carlos's account.

![[Pasted image 20210919181137.png]]

After changing that value, I tried to login to carlos's account. I was able to login to carlos's account using the password of "password1" which means I was able to change his password.

![[Pasted image 20210919181245.png]]