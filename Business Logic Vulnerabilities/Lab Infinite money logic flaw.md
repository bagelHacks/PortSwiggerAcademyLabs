# Lab Infinite money logic flaw

## Objective:

 This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: wiener:peter 

This is the landing page

![[Pasted image 20211018124442.png]]

Updated email to new subdomain

![[Pasted image 20211018125156.png]]

Scrolling to the bottom of the page shows a sign up page

![[Pasted image 20211019100821.png]]

As part of the portswigger labs, I get an email client

![[Pasted image 20211019100922.png]]

I wonder if I can get multiple coupon codes by signing up multiple times?

![[Pasted image 20211019100956.png]]

I signed up using my email address

![[Pasted image 20211019101015.png]]

I received the coupon code of SIGNUP30

![[Pasted image 20211019101039.png]]

wiener@exploit-ac821f071f494753c0af41b001ca0006.web-security-academy.net

wiener@bla.exploit-ac821f071f494753c0af41b001ca0006.web-security-academy.net

Added 99 Leather jackets to my cart

![[Pasted image 20211019101224.png]]

Tested out the coupon 

I lowered the quantity to 1. I wanted to see if the reduction would decrease, and it did.

![[Pasted image 20211019101323.png]]

If the reduction stayed to the same value as having 99 leather jackets, then I would be able to buy the leather jacket for free. 


I went back to the my account page

![[Pasted image 20211019101701.png]]

The gift cards section looks interesting. I entered the SIGNUP30 value. 

![[Pasted image 20211019101729.png]]

![[Pasted image 20211019101745.png]]

Received an error of "Invalid gift card"

![[Pasted image 20211019101804.png]]

I wonder if I can get a gift card code by registering with a new email

I registered with the email of wiener@test.exploit-ac821f071f494753c0af41b001ca0006.web-security-academy.net

Registered again

![[Pasted image 20211019102129.png]]

I did not receive a gift card code in my email

![[Pasted image 20211019102715.png]]

I noticed there is a Gift Card item in the shop

![[Pasted image 20211019102740.png]]

I purchased this item


![[Pasted image 20211019102811.png]]

![[Pasted image 20211019102830.png]]

This had the code of VEnd45VdUc

I tested this code in the Gift cards section

![[Pasted image 20211019103133.png]]

![[Pasted image 20211019103143.png]]

I tried the code again, but I received "Invalid gift card"

Will try buying multiple giftcards. As I was doing this, I noticed that by using the SIGNUP30 coupon code, I would only need to spend 98 dollars for 140 dollars worth of gift card. I can then redeem these gift cards and earn about 40$

![[Pasted image 20211019104006.png]]

I received the following coupon codes

![[Pasted image 20211019104046.png]]

Now, I have to redeem these

![[Pasted image 20211019104127.png]]

I sent this request to intruder to quickly redeem all of the codes

I chose the Gift-card value

![[Pasted image 20211019104209.png]]

For Payloads, I pasted the coupon code values

![[Pasted image 20211019104238.png]]

![[Pasted image 20211019104321.png]]

Once this is completed, I have 142 store credit

![[Pasted image 20211019104350.png]]

I repeated the process, now that I had more store credit I was able to purchase more gift cards

![[Pasted image 20211019104526.png]]

![[Pasted image 20211019104539.png]]

I repeated this until I had enough for the leather jacket

During this time, my community burp intruder would take a long time. I wrote a python script to redeem the codes faster then intruder

![[Pasted image 20211019113340.png]]

![[Pasted image 20211019113357.png]]

Eventually, I had enough credit to buy the jacket 

![[Pasted image 20211019113918.png]]


![[Pasted image 20211019113935.png]]