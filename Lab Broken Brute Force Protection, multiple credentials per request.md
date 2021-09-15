# Lab Broken Brute Force Protection, multiple credentials per request

## Objective: 

This lab is vulnerable due to a logic flaw in it's brute-force protection. To solve the lab, brute-force Carlos's password, then access his account page. 

Victim Username: Carlos

1. Look at what the authentication looks like

![[Pasted image 20210915104917.png]]

![[Pasted image 20210915105005.png]]

![[Pasted image 20210915105014.png]]

![[Pasted image 20210915105025.png]]

2. We are authentication through json... I wonder if we can try multiple different passwords 

I tried sending the following, but received an internal server error

![[Pasted image 20210915105328.png]]

3. I changed the way I sent the password, and it looks like I can send different passwords for the carlos user

![[Pasted image 20210915105452.png]]

4. I used this linux one liner to read the password.txt file and format it for the login request

` for i in $(cat passwords.txt); do echo \"password\":\"$i\"\,; done  `

![[Pasted image 20210915105819.png]]

I copied the output to Repeater

Now the request looks like this.

![[Pasted image 20210915105913.png]]

3. After sending the request, I still received an "Invalid username or password" response. This means I need to try something else. I tried crating a new set of brackets, but this received a 500 internal error.

![[Pasted image 20210915110428.png]]

4. I changed the json a bit and this seems to work

![[Pasted image 20210915111306.png]]

5. I used the following bash 1 liner to read the password.txt file into the json format that seems to work 
`   
for i in $(cat passwords.txt); do echo \"username\":\"Carlos\"\,"\n"\"password\":\"$i\"\,"\n"\"\":\"\"\,; done
  `

![[Pasted image 20210915111813.png]]

6. I copied the password to the request

![[Pasted image 20210915111936.png]]

I still received "Invalid username or password"

![[Pasted image 20210915111955.png]]


6. I will try dropping the "username" argument
`
for i in $(cat passwords.txt); do echo \"password\":\"$i\"\,"\n"\"\":\"\"\,; done
`

![[Pasted image 20210915112213.png]]

I copied the output to burp repeater

![[Pasted image 20210915112332.png]]

I still received "Invalid username or password"

![[Pasted image 20210915112358.png]]


7. I looked at the solution

![[Pasted image 20210915112905.png]]

I had the right idea, but I need to place multiple passwords in the password key 

` for i in $(cat passwords.txt); do echo \"$i\"\,"\n"; done `

![[Pasted image 20210915113202.png]]

I copied the values to the request

![[Pasted image 20210915115051.png]]

This request received a 302 found error which likely means that it worked.

![[Pasted image 20210915115257.png]]