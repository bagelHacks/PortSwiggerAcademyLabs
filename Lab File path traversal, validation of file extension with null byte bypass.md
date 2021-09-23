# Lab File path traversal, validation of file extension with null byte bypass

## Objective:

 This lab contains a file path traversal vulnerability in the display of product images.

The application validates that the supplied filename ends with the expected file extension.

To solve the lab, retrieve the contents of the /etc/passwd file. 

Big idea:

 If an application requires that the user-supplied filename must end with an expected file extension, such as .png, then it might be possible to use a null byte to effectively terminate the file path before the required extension. For example:

filename=../../../etc/passwd%00.png 

This is what the landing page looks like 

![image](https://user-images.githubusercontent.com/90155329/134448494-00e5a47e-9da6-4052-88a4-5937baaca4d5.png)

This lab is targeting a directory traversal vulnerability, so I should look for a good target in the source code.

Reviewing the source code, I noticed that it is calling a local image file.

![image](https://user-images.githubusercontent.com/90155329/134448508-316eb35e-3ed7-446e-a3fb-e25ca13330a2.png)

Visiting the following, I can see the image file.

https://acf31f461f00ed5b805b2b14008b0005.web-security-academy.net/image?filename=21.jpg

![image](https://user-images.githubusercontent.com/90155329/134448525-7404a0a1-bab4-4037-ab01-d7231363f053.png)

To test this page, I sent this request to Burp Repeater. Repeater allows me to quickly test different payloads.

![image](https://user-images.githubusercontent.com/90155329/134448537-b32bd1a7-4915-4abd-9f5b-f44745b700b5.png)

I tried a payload of "../../../../../etc/passwd" and received 'No such file' as the response.

![image](https://user-images.githubusercontent.com/90155329/134448549-67820584-c0c9-4fe7-a1be-1d92a71490a7.png)

Next, I appended a null byte (%00) to the end of the payload and received "No such file"


../../../../../etc/passwd%00

![image](https://user-images.githubusercontent.com/90155329/134448566-161cf3ef-f77f-4d88-983f-6771a9da3def.png)

Next, I tried the following payload and it worked!

../../../../etc/passwd%00.png


![image](https://user-images.githubusercontent.com/90155329/134448592-c60d600d-34a1-4e65-9712-387f54a5160e.png)

It looks like the webapplication requires the .png file extension. Since we added the null byte, then the web application looks for file /etc/passwd instead of /etc/passwd.png

![image](https://user-images.githubusercontent.com/90155329/134448613-659ae81a-11a3-4afc-97a9-bcbaae6fcedc.png)

