# Lab File path traversal, validation of file extension with null byte bypass

## Objective:

 This lab contains a file path traversal vulnerability in the display of product images.

The application validates that the supplied filename ends with the expected file extension.

To solve the lab, retrieve the contents of the /etc/passwd file. 

Big idea:

 If an application requires that the user-supplied filename must end with an expected file extension, such as .png, then it might be possible to use a null byte to effectively terminate the file path before the required extension. For example:

filename=../../../etc/passwd%00.png 

This is what the landing page looks like 

![[Pasted image 20210922223520.png]]

This lab is targeting a directory traversal vulnerability, so I should look for a good target in the source code.

Reviewing the source code, I noticed that it is calling a local image file.

![[Pasted image 20210922223829.png]]

Visiting the following, I can see the image file.

https://acf31f461f00ed5b805b2b14008b0005.web-security-academy.net/image?filename=21.jpg

![[Pasted image 20210922223856.png]]

To test this page, I sent this request to Burp Repeater. Repeater allows me to quickly test different payloads.

![[Pasted image 20210922224004.png]]

I tried a payload of "../../../../../etc/passwd" and received 'No such file' as the response.

![[Pasted image 20210922224058.png]]

Next, I appended a null byte (%00) to the end of the payload and received "No such file"


../../../../../etc/passwd%00

![[Pasted image 20210922224226.png]]

Next, I tried the following payload and it worked!

../../../../etc/passwd%00.png


![[Pasted image 20210922224321.png]]

It looks like the webapplication requires the .png file extension. Since we added the null byte, then the web application looks for file /etc/passwd instead of /etc/passwd.png

![[Pasted image 20210922224410.png]]

