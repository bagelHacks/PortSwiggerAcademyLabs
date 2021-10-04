# Lab Weak isolation on dual-user endpoint

## Objective:

This lab makes a flawed assumption about the user's privilege level based on their input. As a result, you can exploit the logic of its account management features to gain access to arbitrary users' accounts. To solve the lab, access the `administrator` account and delete Carlos.

You can log in to your own account using the following credentials: `wiener:peter`

------------------------------------------------------------

I started by logging in with the wiener:peter account


![[Pasted image 20211004023106.png]]

After logging in, I was redirected to this page 

![[Pasted image 20211004023203.png]]

After logging in, I tried to access the /admin page. Since I am not an administrator, I was not able to access this page 

![[Pasted image 20211004023242.png]]

I will try changing my email. I intercepted the POST request to see what the variable/arguments look like. Sometimes this is a great place to test business logic vulnerabilities.

![[Pasted image 20211004023355.png]]

![[Pasted image 20211004023414.png]]


The body arguments do not look related to my current privileges. I will change my password and I will intercept the request. 

![[Pasted image 20211004023520.png]]

![[Pasted image 20211004023553.png]]

I will modify the request by getting rid of the username value

![[Pasted image 20211004023627.png]]

I received the response "current password is incorrect"

![[Pasted image 20211004023708.png]]

I tried changing the username to Admin, and getting rid of the current password body argument

![[Pasted image 20211004023910.png]]

This had a response of "user does not exist"

![[Pasted image 20211004024037.png]]

I will do the same, but with a "admin" instead of "Admin"

![[Pasted image 20211004024205.png]]

Received another "user does not exist" error

![[Pasted image 20211004024330.png]]

I will try the same with the "Administrator" account

![[Pasted image 20211004024420.png]]

Like before, I dropped the "Current password" body variable

![[Pasted image 20211004024456.png]]

I received response, "Password changed successfully"

![[Pasted image 20211004024519.png]]

I tried logging in with the credentials of administrator:test

![[Pasted image 20211004024639.png]]

This was successful. I was able to visit the /admin page

![[Pasted image 20211004024704.png]]

Whoohoo!

![[Pasted image 20211004024715.png]]