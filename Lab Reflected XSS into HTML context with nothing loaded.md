# Lab Reflected XSS into HTML context with nothing loaded


### Objective:
This lab contains a simple reflected cross-site scripting vulnerability in the search functionality. To solve the lab, perform a cross-site scripting attack that calls the alert function. 

This is the landing page.

This search bar looks interesting to attack.

![[Pasted image 20210911133132.png]]

Entering the string of "TestingTesting", we can see this user inputed value is populated in the next screen

![[Pasted image 20210911133438.png]]

I can also see that my user input was added to the URL

![[Pasted image 20210911133521.png]]

This looks like a good place to try and run javascript to perform a XSS attack.

I used the simple payload of `<script>alert(1)<script>`
	
![[Pasted image 20210911133644.png]]
	
An alert was generated with solved the challenge:

![[Pasted image 20210911133745.png]]