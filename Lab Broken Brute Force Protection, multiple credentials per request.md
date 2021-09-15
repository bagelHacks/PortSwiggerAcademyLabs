# Lab Broken Brute Force Protection, multiple credentials per request

## Objective: 

This lab is vulnerable due to a logic flaw in it's brute-force protection. To solve the lab, brute-force Carlos's password, then access his account page. 

Victim Username: carlos

1. Look at what the authentication looks like

![image](https://user-images.githubusercontent.com/90155329/133467596-0108c7cb-7bf6-497a-b18e-a1cfb105a794.png)

![image](https://user-images.githubusercontent.com/90155329/133467622-5bb61152-e11b-40c6-ab58-2b90fb2e3882.png)

![image](https://user-images.githubusercontent.com/90155329/133467674-11a89eec-c102-4232-acb5-6bf44be1fba0.png)

![image](https://user-images.githubusercontent.com/90155329/133467705-1073a417-0034-4e25-b82d-097a38476fcf.png)

2. We are authentication through json... I wonder if we can try multiple different passwords 

I tried sending the following, but received an internal server error

![image](https://user-images.githubusercontent.com/90155329/133467737-bc23d6c7-5c89-4301-969e-317a42a1e724.png)

3. I changed the way I sent the password, and it looks like I can send different passwords for the carlos user

![image](https://user-images.githubusercontent.com/90155329/133467769-dc3fceb3-f5fa-4737-b318-887c7d524bdd.png)

4. I used this linux one liner to read the password.txt file and format it for the login request

` for i in $(cat passwords.txt); do echo \"password\":\"$i\"\,; done  `

![image](https://user-images.githubusercontent.com/90155329/133467820-5e4d86cb-7ffb-4ed4-acc6-b9123706e2bb.png)

I copied the output to Repeater

Now the request looks like this.

![image](https://user-images.githubusercontent.com/90155329/133468074-54ab3654-ed18-4526-a4e7-8155ed6eed8b.png)

5. After sending the request, I still received an "Invalid username or password" response. This means I need to try something else. I tried crating a new set of brackets, but this received a 500 internal error.

![image](https://user-images.githubusercontent.com/90155329/133468133-c7aa0059-30a2-4619-86a3-2d4a9ec51242.png)

6. I changed the json a bit and this seems to work

![image](https://user-images.githubusercontent.com/90155329/133468162-97726974-93e8-4f62-a66c-24896a2ebea8.png)

7. I used the following bash 1 liner to read the password.txt file into the json format that seems to work 

`   
for i in $(cat passwords.txt); do echo \"username\":\"Carlos\"\,"\n"\"password\":\"$i\"\,"\n"\"\":\"\"\,; done
  `

![image](https://user-images.githubusercontent.com/90155329/133468214-dab3b4d0-90b5-475b-885b-317307cb6e8c.png)

8. I copied the password to the request

![[Pasted image 20210915111936.png]]

I still received "Invalid username or password"

![image](https://user-images.githubusercontent.com/90155329/133468260-fa64d741-58d9-4e12-a5ec-9fb59c2118c2.png)


9. I will try dropping the "username" argument
`
for i in $(cat passwords.txt); do echo \"password\":\"$i\"\,"\n"\"\":\"\"\,; done
`

![image](https://user-images.githubusercontent.com/90155329/133468458-e6574318-f186-4c37-b58e-7bc839b35642.png)

I copied the output to burp repeater

![image](https://user-images.githubusercontent.com/90155329/133468493-affbeefc-fce3-4a51-94cd-02792512751e.png)

I still received "Invalid username or password"

![image](https://user-images.githubusercontent.com/90155329/133468522-63da673c-6f98-417f-9746-8c6a23e063dc.png)


10. I looked at the solution

![image](https://user-images.githubusercontent.com/90155329/133468554-98ad92ab-ec1c-4bdc-9cdc-7845b71d1503.png)

I had the right idea, but I need to place multiple passwords in the password key 

` for i in $(cat passwords.txt); do echo \"$i\"\,"\n"; done `

![image](https://user-images.githubusercontent.com/90155329/133468587-94f11654-a4a5-48c5-b039-468442020f62.png)

I copied the values to the request

![image](https://user-images.githubusercontent.com/90155329/133468626-952d3640-d57e-4f64-a356-50442453300c.png)

This request received a 302 found error which likely means that it worked.

![image](https://user-images.githubusercontent.com/90155329/133468671-8e8ea9dd-fd5d-47b8-8a46-53cde41680c0.png)
