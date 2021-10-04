# Lab Inconsistent security controls

## Objective: 

This lab's flawed logic allows arbitrary users to access administrative functionality that should only be available to company employees. To solve the lab, access the admin panel and delete Carlos.

## Big Idea"

Applications may appear to be secure because they implement seemingly robust measures to enforce the business rules. Unfortunately, some applications make the mistake of assuming that, having passed these strict controls initially, the user and their data can be trusted indefinitely. This can result in relatively lax enforcement of the same controls from that point on.

If business rules and security measures are not applied consistently throughout the application, this can lead to potentially dangerous loopholes that may be exploited by an attacker.

--------------------------------------------


This is what the register account page looks like

![image](https://user-images.githubusercontent.com/90155329/135807204-d267422b-03c6-4cd8-8482-b50325c5e67b.png)

I do not have control of the "dontwannacry" email domain, but I do have control of the exploit-ac7a1f3d1fe06918809008cc018100fb.web-security-academy.net domain.

I started by registering with the following account.

![image](https://user-images.githubusercontent.com/90155329/135807226-3fb90398-087f-4c37-8f01-725fc87a2839.png)

From my email client, I received a verification link

![image](https://user-images.githubusercontent.com/90155329/135807245-8d872e3a-5c9f-450a-9298-810a3b02120c.png)

After I verified my account, I was able to login with the registered account

![image](https://user-images.githubusercontent.com/90155329/135807265-a66dbb79-df8c-4e46-a140-bc794f368dbe.png)

After logging in, I was welcomed by the following page.

![image](https://user-images.githubusercontent.com/90155329/135807283-63f6208d-e702-4559-a300-107da1abe393.png)

I visited /admin to see if I had access. Unfortunately, I did not have access because I do not have a dontwannacry email address

![image](https://user-images.githubusercontent.com/90155329/135807300-365238fc-1cb7-4669-8a97-6976dde61ee6.png)

I will try changing my email address to hacker@dontwannacry.com

![image](https://user-images.githubusercontent.com/90155329/135807323-74ff1193-38f4-4fdf-9081-8523031e5831.png)

![image](https://user-images.githubusercontent.com/90155329/135807356-5e7bb5fc-b8ba-4cd4-8c2a-04ece4e97578.png)

Now, that I changed my email, I was able to visit the /admin page 

![image](https://user-images.githubusercontent.com/90155329/135807376-9d421903-312d-429a-acdd-32d8abc783bc.png)

![image](https://user-images.githubusercontent.com/90155329/135807417-85664e3b-65f8-4530-8de6-5dbb3626a00c.png)
