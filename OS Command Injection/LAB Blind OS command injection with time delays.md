# LAB Blind OS command injection with time delays

## Objective 

This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response.

To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay. 

## Big Idea 

 You can use an injected command that will trigger a time delay, allowing you to confirm that the command was executed based on the time that the application takes to respond. The ping command is an effective way to do this, as it lets you specify the number of ICMP packets to send, and therefore the time taken for the command to run:

& ping -c 10 127.0.0.1 &

This command will cause the application to ping its loopback network adapter for 10 seconds. 

This is what the lab landing page looks like 

![image](https://user-images.githubusercontent.com/90155329/135767679-8864efeb-2ac9-4d3b-80b4-1ce32b0c7d4e.png)

I went to "Submit feedback" and the following page returned

![image](https://user-images.githubusercontent.com/90155329/135767688-7e1569e5-9bd7-4e20-9311-c8f89ae8842a.png)

Since this is the piece that is vulnerable to command injection, I will intercept a request with Burp Intercept. 

![image](https://user-images.githubusercontent.com/90155329/135767705-e2bc8440-7a55-4ab7-a4b3-db9b07bc8a01.png)

This is what the request looks like

![image](https://user-images.githubusercontent.com/90155329/135767716-ecfe435c-c419-402d-8203-07c53dacd8d7.png)

I added a command to the "email" value. The following payload seems to work

csrf=NFxkVlRCSVLoeZNZvDd1weCzuZsE3dMo&name=bagelHacks&email=bagelHacks%40hacker.hacker;ping+-c+20+127.0.0.1+%26&subject=Tesing&message=testtest

After url decoding, it is the following 

csrf=NFxkVlRCSVLoeZNZvDd1weCzuZsE3dMo&name=bagelHacks&email=bagelHacks@hacker.hacker;ping -c 20 127.0.0.1 &&subject=Tesing&message=testtest

After sending the payload, the application did not respond for about 20 seconds.

This means that the application pinged 127.0.0.1 20 times successfully.

![image](https://user-images.githubusercontent.com/90155329/135767723-927a5406-afc4-4b26-a0ff-27ae2d649378.png)
