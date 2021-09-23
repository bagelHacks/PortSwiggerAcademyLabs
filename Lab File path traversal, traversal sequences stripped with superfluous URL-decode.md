# Lab File path traversal, traversal sequences stripped with superfluous URL-decode

Non-standard encodings such as ..%c0%af or ..%252f can be used to bypass the input filter. 

I used the following article as a reference:

https://security.stackexchange.com/questions/48879/why-does-directory-traversal-attack-c0af-work

## Objective:

 This lab contains a file path traversal vulnerability in the display of product images.

The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it.

To solve the lab, retrieve the contents of the /etc/passwd file. 

This is what the LAB webpage looks like

![[Pasted image 20210922215234.png]]

Notice the images. Looking at the source code of the welcome page, I can see the img header calling a local file.

![[Pasted image 20210922215319.png]]

Visiting that link shows the following

![[Pasted image 20210922215337.png]]


8.jpg is a local file and is likely where the path traversal is. 

I intercepted this request in Burp intercept

![[Pasted image 20210922215429.png]]

I tried the payload of /etc/passwd and received "No such file"

![[Pasted image 20210922215458.png]]

I tried the payload of ../../../../../../etc/passwd and received "Protocol error"

![[Pasted image 20210922215839.png]]

I tried the following payload and receive "Protocol error". `%c0%af` is not a valid unicode character and some web applications handle this value as \

..%c0%af..%c0%af..%c0%af..%c0%af..%c0%af..%c0%afetc%c0%afpasswd

![[Pasted image 20210922215725.png]]


Just like before `%252f` is not a valid unicode character and some web applications handle this value as \

I tried the following payload

`..%252f..%252f..%252f..%252f..%252f..%252fetc%252fpasswd `

This was successful and we were able to read /etc/passwd

![[Pasted image 20210922220453.png]]

![[Pasted image 20210922220526.png]]