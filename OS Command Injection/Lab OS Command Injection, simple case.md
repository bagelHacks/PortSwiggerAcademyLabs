# Lab OS Command Injection, simple case

## Objective:

 This lab contains an OS command injection vulnerability in the product stock checker.

The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response.

To solve the lab, execute the whoami command to determine the name of the current user. 

This is what the lab landing page looks like.

![image](https://user-images.githubusercontent.com/90155329/135767514-0e940f4c-23f8-467a-945b-796071d6b5a5.png)

After playing with the application, I found the product stock checker functionality in one of the product pages

![image](https://user-images.githubusercontent.com/90155329/135767519-538a0b62-f5a0-4212-a85b-4b8bb9608d05.png)

Clicking "Check stock" returned the value of "62 units"

![image](https://user-images.githubusercontent.com/90155329/135767534-fe89cd7a-2fbe-44aa-8b4a-bef81187c668.png)

I am interested to see this from Burp. I intercepted the request with Burp Intruder.

![image](https://user-images.githubusercontent.com/90155329/135767539-0d5bd2d5-09d6-4191-b12d-8abf69319f77.png)

Notice that the productID and storeID value look like they can be modified. 

I sent the request to Burp Repeater. Repeater lets me to modify and test different requests.

![image](https://user-images.githubusercontent.com/90155329/135767545-b84b20ed-534d-43e5-bb0d-a86ff266439d.png)

Since this is vulnerable to command injection, there is likley a system command running in the background that takes in the prodcuctID and storeID values to calculate the output number

I will try adding the command of "whoami"

1;whoami

I received an error "whoami not found"

![image](https://user-images.githubusercontent.com/90155329/135767550-42d1d3cc-368f-4374-acf3-2c4dcb7ccb62.png)



adding the ` ; ` value finnished the first command used by the application, and allowed the "whoami" command to execute

The error means I attempted to execute a command that did not exist. 

I changed the payload to the following which worked

productId=1&storeId=1;whoami

![image](https://user-images.githubusercontent.com/90155329/135767559-eef372cd-55b4-479a-abca-fd1835d717e6.png)

![image](https://user-images.githubusercontent.com/90155329/135767566-21224b8d-6fde-4057-97a3-d8f3348664a3.png)

