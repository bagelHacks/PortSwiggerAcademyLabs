# Lab Reflected XSS into HTML context with nothing loaded


### Objective:
This lab contains a simple reflected cross-site scripting vulnerability in the search functionality. To solve the lab, perform a cross-site scripting attack that calls the alert function. 

This is the landing page.

This search bar looks interesting to attack.

![image](https://user-images.githubusercontent.com/90155329/132958785-518404b1-2c91-45f7-a4e0-ef80caea2095.png)

Entering the string of "TestingTesting", we can see this user inputed value is populated in the next screen

![image](https://user-images.githubusercontent.com/90155329/132958798-6e521d54-2214-421e-8ede-999fd2991a2d.png)

I can also see that my user input was added to the URL

![image](https://user-images.githubusercontent.com/90155329/132958803-6959e965-4ba1-46b2-afe6-6c38040deb80.png)

This looks like a good place to try and run javascript to perform a XSS attack.

I used the simple payload of `<script>alert(1)<script>`
	
![image](https://user-images.githubusercontent.com/90155329/132958808-e7a473d2-d54b-45e3-b990-65a79f426fed.png)
	
An alert was generated with solved the challenge:

![image](https://user-images.githubusercontent.com/90155329/132958814-834ebc64-a0ed-4457-9bda-a26453e60ca6.png)
