# Lab File path traversal, traversal sequences stripped with superfluous URL-decode

Non-standard encodings such as ..%c0%af or ..%252f can be used to bypass the input filter. 

I used the following article as a reference:

https://security.stackexchange.com/questions/48879/why-does-directory-traversal-attack-c0af-work

## Objective:

 This lab contains a file path traversal vulnerability in the display of product images.

The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it.

To solve the lab, retrieve the contents of the /etc/passwd file. 

This is what the LAB webpage looks like

![image](https://user-images.githubusercontent.com/90155329/134445340-7e917fdc-7eda-498a-a0c3-8e08a8f81669.png)

Notice the images. Looking at the source code of the welcome page, I can see the img header calling a local file.

![image](https://user-images.githubusercontent.com/90155329/134445354-0913f19a-5e16-47b6-8205-1894ae1b94b9.png)

Visiting that link shows the following

![image](https://user-images.githubusercontent.com/90155329/134445374-6d487d6b-b125-411f-9319-0f693c4ec1a7.png)


8.jpg is a local file and is likely where the path traversal is. 

I intercepted this request in Burp intercept

![image](https://user-images.githubusercontent.com/90155329/134445385-18773abb-88a6-44c4-972e-4749354f4dd1.png)

I tried the payload of /etc/passwd and received "No such file"

![image](https://user-images.githubusercontent.com/90155329/134445398-3e000cdd-9004-48e9-8ce2-bb3bd2c963bc.png)

I tried the payload of ../../../../../../etc/passwd and received "Protocol error"

![image](https://user-images.githubusercontent.com/90155329/134445431-f0cabe60-ac92-4d31-bc61-bea07a8f320c.png)

I tried the following payload and receive "Protocol error". `%c0%af` is not a valid unicode character and some web applications handle this value as \

..%c0%af..%c0%af..%c0%af..%c0%af..%c0%af..%c0%afetc%c0%afpasswd

![image](https://user-images.githubusercontent.com/90155329/134445449-5eab2152-a35a-4742-933d-23ff367ef756.png)


Just like before `%252f` is not a valid unicode character and some web applications handle this value as \

I tried the following payload

`..%252f..%252f..%252f..%252f..%252f..%252fetc%252fpasswd `

This was successful and we were able to read /etc/passwd

![image](https://user-images.githubusercontent.com/90155329/134445462-569d7a03-8475-4aec-a164-3fe853caee98.png)

![image](https://user-images.githubusercontent.com/90155329/134445474-0048b477-7dd5-4080-9645-1b05e0fb0515.png)
