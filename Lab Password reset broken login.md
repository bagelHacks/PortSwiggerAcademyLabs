# Lab Password reset broken login

Objective:

 This lab's password reset functionality is vulnerable. To solve the lab, reset Carlos's password then log in and access his "My account" page.

    Your credentials: wiener:peter
    Victim's username: carlos

This lab involves attacking the "Forgot password" functionality

![image](https://user-images.githubusercontent.com/90155329/133944770-823eb5b0-6b9a-4ad5-bfff-91e684a17221.png)

Since, I have credentials to a valid account, I will try resetting their password. Analyzing this process may uncover how this functionality can be attacked.

![image](https://user-images.githubusercontent.com/90155329/133944773-4e03277e-e299-4a77-b8cd-c677d4f539fe.png)

Submitting this password reset request sent a password reset link the wiener's email

![image](https://user-images.githubusercontent.com/90155329/133944780-56a315ab-3867-4b05-b08f-40f883a99814.png)

This is the password reset link that was provided.

https://acb01f361fcff14380240af3005a002c.web-security-academy.net/forgot-password?temp-forgot-password-token=fMUIRtiGNFyrJ6hrL4ApKZEojuuJ4HtT

The link brought me to a password reset page:

![image](https://user-images.githubusercontent.com/90155329/133944801-dbdf470b-14ec-471c-897e-5fe99abc2dd2.png)

The base64 value of "fMUIRtiGNFyrJ6hrL4ApKZEojuuJ4HtT" looks interesting.

I wonder if I can reset a password by deleting the token value 

I tried to reset the password, and intercepted the post request

![image](https://user-images.githubusercontent.com/90155329/133944807-e6115fa0-2c80-41d8-88b0-0f04b41b1add.png)

![image](https://user-images.githubusercontent.com/90155329/133944842-c955e052-1424-41de-a711-6d98aaeabb98.png)

This is interesting. I wonder, if I can modify the username value to change the value of carlos's account.

![image](https://user-images.githubusercontent.com/90155329/133944865-d85c90ff-65e1-41ea-811f-82e5b57cc23d.png)

After changing that value, I tried to login to carlos's account. I was able to login to carlos's account using the password of "password1" which means I was able to change his password.

![image](https://user-images.githubusercontent.com/90155329/133944876-31c68417-5fbc-42ac-bdca-bc2a88ea531f.png)
