# Lab Username enumeration via account lock

## Objective:

This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 

1. Start by figuring out what an authentication looks like 

![image](https://user-images.githubusercontent.com/90155329/133450123-2483382f-bdc4-4911-b560-56f58d050c01.png)

![image](https://user-images.githubusercontent.com/90155329/133450167-0c727084-6206-41fa-8956-fc8329b5eae3.png)

"In valid username or password"

![image](https://user-images.githubusercontent.com/90155329/133450216-ac82fee4-ce02-48a2-946e-565df8f9d915.png)

![image](https://user-images.githubusercontent.com/90155329/133450242-87fb0be0-dd10-43db-b90c-3843be3fa5f6.png)

I will try the list of users:

-  Send the post request to Intruder
-  user the usernames list 
-  sniper
![image](https://user-images.githubusercontent.com/90155329/133450280-4136ae61-927d-41a4-96cd-af521581ed21.png)

![image](https://user-images.githubusercontent.com/90155329/133450314-b63bbf40-8694-46a2-b643-938ce53ca618.png)

![image](https://user-images.githubusercontent.com/90155329/133450359-dddf7d05-19cd-41bf-875f-2193aac9885a.png)

![image](https://user-images.githubusercontent.com/90155329/133450421-5b2e0b40-aba6-435b-9dfd-ea299bbfaee0.png)

After running the attack, every user received a "Invalid username or password"

![image](https://user-images.githubusercontent.com/90155329/133450457-0151d5af-2389-40d8-b3b0-e51a9e140e88.png)

I will try repeat this attack 2 more times to see if it will lock any accounts

After I repeated the attack 4 times, the "apps" account received a slightly longer length and did not receive the "Invalid username or password" error

![image](https://user-images.githubusercontent.com/90155329/133450508-be5612d6-6896-4f03-8892-eef43c5e42d1.png)

Instead, the error was "You made too many incorrect login attempts. Please try again in 1 minute"

![image](https://user-images.githubusercontent.com/90155329/133450540-35ab650f-5874-481a-a69f-f1935c9f6f0d.png)

This means that "apps" is a valid account. 

So it is 3 failed logins then a lockout for 1 minute 

I went back to intruder and changed the payload position

![image](https://user-images.githubusercontent.com/90155329/133450582-5e4ce78d-b7d7-42d8-85af-35cc8b744f8e.png)

For the payload options, I loaded the password.txt file 

![image](https://user-images.githubusercontent.com/90155329/133450616-48539e9c-9799-449e-b91c-d4872268e155.png)

I used the "Resource Pool" tab to select wait 1 minute after 3 requests

![image](https://user-images.githubusercontent.com/90155329/133450657-718b88d1-1bc7-45db-94cb-51f6d993d90e.png)

As this was going on, I wrote a python script that would do the same 


![image](https://user-images.githubusercontent.com/90155329/133450778-680c48f1-a2fa-4ed6-a6e7-156966251785.png)



Eventually, it looks like the password of "chelsea" worked!

![image](https://user-images.githubusercontent.com/90155329/133450855-0e7c18af-fce1-44a7-a766-17052e67599f.png)

![image](https://user-images.githubusercontent.com/90155329/133450896-f8bc6ab3-9fb9-44c1-aeed-36808eb5136a.png)
