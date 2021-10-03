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

![[Pasted image 20210922233306.png]]

I went to "Submit feedback" and the following page returned

![[Pasted image 20210922233340.png]]

Since this is the piece that is vulnerable to command injection, I will intercept a request with Burp Intercept. 

![[Pasted image 20210922233428.png]]

This is what the request looks like

![[Pasted image 20210922233451.png]]

I added a command to the "email" value. The following payload seems to work

csrf=NFxkVlRCSVLoeZNZvDd1weCzuZsE3dMo&name=bagelHacks&email=bagelHacks%40hacker.hacker;ping+-c+20+127.0.0.1+%26&subject=Tesing&message=testtest

After url decoding, it is the following 

csrf=NFxkVlRCSVLoeZNZvDd1weCzuZsE3dMo&name=bagelHacks&email=bagelHacks@hacker.hacker;ping -c 20 127.0.0.1 &&subject=Tesing&message=testtest

After sending the payload, the application did not respond for about 20 seconds.

This means that the application pinged 127.0.0.1 20 times successfully.

![[Pasted image 20210922233836.png]]