# Lab Username enumeration via account lock

## Objective:

This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 

1. Start by figuring out what an authentication looks like 

![[Pasted image 20210915082930.png]]

![[Pasted image 20210915082957.png]]

"In valid username or password"

![[Pasted image 20210915083050.png]]

![[Pasted image 20210915083101.png]]

I will try the list of users:

-  Send the post request to Intruder
-  user the usernames list 
-  sniper
![[Pasted image 20210915083349.png]]

![[Pasted image 20210915083431.png]]

![[Pasted image 20210915083456.png]]

![[Pasted image 20210915083552.png]]

After running the attack, every user received a "Invalid username or password"

![[Pasted image 20210915083716.png]]

I will try repeat this attack 2 more times to see if it will lock any accounts

After I repeated the attack 4 times, the "apps" account received a slightly longer length and did not receive the "Invalid username or password" error

![[Pasted image 20210915084003.png]]

Instead, the error was "You made too many incorrect login attempts. Please try again in 1 minute"

![[Pasted image 20210915084035.png]]

This means that "apps" is a valid account. 

So it is 3 failed logins then a lockout for 1 minute 

I went back to intruder and changed the payload position

![[Pasted image 20210915084344.png]]

For the payload options, I loaded the password.txt file 

![[Pasted image 20210915084409.png]]

I used the "Resource Pool" tab to select wait 1 minute after 3 requests

![[Pasted image 20210915084844.png]]

As this was going on, I wrote a python script that would do the same 


![[Pasted image 20210915101232.png]]



Eventually, it looks like the password of "chelsea" worked!

![[Pasted image 20210915101213.png]]

![[Pasted image 20210915101341.png]]