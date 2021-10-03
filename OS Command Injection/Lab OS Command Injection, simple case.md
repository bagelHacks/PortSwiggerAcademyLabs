# Lab OS Command Injection, simple case

## Objective:

 This lab contains an OS command injection vulnerability in the product stock checker.

The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response.

To solve the lab, execute the whoami command to determine the name of the current user. 

This is what the lab landing page looks like.

![[Pasted image 20210922230539.png]]

After playing with the application, I found the product stock checker functionality. in one of the product pages

![[Pasted image 20210922230705.png]]

Clicking "Check stock" returned the value of "62 units"

![[Pasted image 20210922230737.png]]

I am interested to see this from Burp. I intercepted the request with Burp Intruder.

![[Pasted image 20210922230822.png]]

Notice that the productID and storeID value look like they can be modified. 

I sent the request to Burp Repeater. Repeater lets me to modify and test different requests.

![[Pasted image 20210922230921.png]]

Since this is vulnerable to command injection, there is likley a system command running in the background that takes in the prodcuctID and storeID values to calculate the output number

I will try adding the command of "whoami"

1;whoami

I received an error "whoami not found"

![[Pasted image 20210922232504.png]]



adding the ` ; ` value finnished the first command used by the application, and allowed the "whoami" command to execute

The error means I attempted to execute a command that did not exist. 

I changed the payload to the following which worked

productId=1&storeId=1;whoami

![[Pasted image 20210922232717.png]]

![[Pasted image 20210922232725.png]]

