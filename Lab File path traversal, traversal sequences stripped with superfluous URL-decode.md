# Lab File path traversal, traversal sequences stripped with superfluous URL-decode

Non-standard encodings such as ..%c0%af or ..%252f can be used to bypass the input filter. 

I used the following article as a reference:

https://security.stackexchange.com/questions/48879/why-does-directory-traversal-attack-c0af-work

## Objective:

 This lab contains a file path traversal vulnerability in the display of product images.

The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it.

To solve the lab, retrieve the contents of the /etc/passwd file. 

This is what the LAB webpage looks like

![image](https://user-images.githubusercontent.com/90155329/134448183-bf5be7db-c10c-4fa0-829c-e40933d8a50e.png)

Notice the images. Looking at the source code of the welcome page, I can see the img header calling a local file.

![image](https://user-images.githubusercontent.com/90155329/134448211-47fb8b21-07ac-4626-9158-f11150c21287.png)

Visiting that link shows the following

![image](https://user-images.githubusercontent.com/90155329/134448232-286be110-2c84-4224-99c7-ae92ae8e1fb4.png)

8.jpg is a local file and is likely where the path traversal is. 

I intercepted this request in Burp intercept

![image](https://user-images.githubusercontent.com/90155329/134448256-aa5a27f8-c7c7-401a-a849-72b0367ab7b5.png)

I tried the payload of /etc/passwd and received "No such file"

![image](https://user-images.githubusercontent.com/90155329/134448273-5333ea74-5137-471d-b104-e2add94315c4.png)

I tried the payload of ../../../../../../etc/passwd and received "Protocol error"

![image](https://user-images.githubusercontent.com/90155329/134448293-239a452c-88d9-4d5b-9939-d661794f9bc4.png)

I tried the following payload and receive "Protocol error". `%c0%af` is not a valid unicode character and some web applications handle this value as \

..%c0%af..%c0%af..%c0%af..%c0%af..%c0%af..%c0%afetc%c0%afpasswd

![image](https://user-images.githubusercontent.com/90155329/134448311-befdcafd-c203-4ff5-a08f-f12ba2902888.png)


Just like before `%252f` is not a valid unicode character and some web applications handle this value as \

I tried the following payload

`..%252f..%252f..%252f..%252f..%252f..%252fetc%252fpasswd `

This was successful and we were able to read /etc/passwd

![image](https://user-images.githubusercontent.com/90155329/134448345-48e932c6-d74c-43dd-8e16-330ce19417c7.png)

![image](https://user-images.githubusercontent.com/90155329/134448356-94202084-78a9-4473-8501-0aa84724e80e.png)
