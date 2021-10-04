# Lab Weak isolation on dual-user endpoint

## Objective:

This lab makes a flawed assumption about the user's privilege level based on their input. As a result, you can exploit the logic of its account management features to gain access to arbitrary users' accounts. To solve the lab, access the `administrator` account and delete Carlos.

You can log in to your own account using the following credentials: `wiener:peter`

------------------------------------------------------------

I started by logging in with the wiener:peter account


![image](https://user-images.githubusercontent.com/90155329/135807621-9ebc0b43-f842-467a-810f-d82490b73410.png)

After logging in, I was redirected to this page 

![image](https://user-images.githubusercontent.com/90155329/135807642-507ccc20-e357-4739-b0e6-848573dfda0e.png)

After logging in, I tried to access the /admin page. Since I am not an administrator, I was not able to access this page 

![image](https://user-images.githubusercontent.com/90155329/135807669-a5af3ec4-3536-4999-814e-4c41176cfe3f.png)

I will try changing my email. I intercepted the POST request to see what the variable/arguments look like. Sometimes this is a great place to test business logic vulnerabilities.

![image](https://user-images.githubusercontent.com/90155329/135807691-aa3d27b5-56cd-41e2-b18d-4b29cd12f2c8.png)

![image](https://user-images.githubusercontent.com/90155329/135807710-bdd84996-5925-4021-ab74-6cc222302e00.png)


The body arguments do not look related to my current privileges. I will change my password and I will intercept the request. 

![image](https://user-images.githubusercontent.com/90155329/135807738-c7891b55-9c76-4072-b6f6-c1e4fec0205c.png)

![image](https://user-images.githubusercontent.com/90155329/135807766-19a05803-ba47-49e9-83a2-816d11438538.png)

I will modify the request by getting rid of the username value

![image](https://user-images.githubusercontent.com/90155329/135807785-4aad1ede-355d-4c13-8189-b397bd025e62.png)

I received the response "current password is incorrect"

![image](https://user-images.githubusercontent.com/90155329/135807805-5de72033-2e37-48ac-a9d3-d33561482b02.png)

I tried changing the username to Admin, and getting rid of the current password body argument

![image](https://user-images.githubusercontent.com/90155329/135807874-9a2b2493-2ef7-4d1a-832b-9084444d72fb.png)

This had a response of "user does not exist"

![image](https://user-images.githubusercontent.com/90155329/135807848-8c56f38e-67ce-4063-829b-c187f26f1baa.png)

I will do the same, but with a "admin" instead of "Admin"

![image](https://user-images.githubusercontent.com/90155329/135807892-b140a9f5-e05b-44a5-ab6e-1d8b6c6efb10.png)

Received another "user does not exist" error

![image](https://user-images.githubusercontent.com/90155329/135807919-f567b5bd-7e61-48e1-932a-0e8d052df082.png)

I will try the same with the "Administrator" account

![image](https://user-images.githubusercontent.com/90155329/135807942-01346e57-e53f-442b-8882-51010c190b0c.png)

Like before, I dropped the "Current password" body variable

![image](https://user-images.githubusercontent.com/90155329/135807955-22d6ddbe-96f5-4df1-8aeb-6d0d3506833b.png)

I received response, "Password changed successfully"

![image](https://user-images.githubusercontent.com/90155329/135807982-ea61265a-d2d8-4c80-9273-18b82dc75790.png)

I tried logging in with the credentials of administrator:test

![image](https://user-images.githubusercontent.com/90155329/135808014-f490e7e8-badf-4ee4-a74a-01856a67826f.png)

This was successful. I was able to visit the /admin page

![image](https://user-images.githubusercontent.com/90155329/135808034-e0d56c77-a437-466b-9a09-805d31afaa87.png)

Whoohoo!

![image](https://user-images.githubusercontent.com/90155329/135808048-e417dad6-1742-4a70-9fb6-792ea21fb6a4.png)
