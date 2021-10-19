# Lab Infinite money logic flaw

## Objective:

 This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: wiener:peter 

This is the landing page

![image](https://user-images.githubusercontent.com/90155329/137952762-6de7a910-b8d4-4482-a504-b6bb7a866f36.png)

Updated email to new subdomain

![image](https://user-images.githubusercontent.com/90155329/137952791-26d4169a-0b34-4ba1-886f-3c85657bb9d5.png)

Scrolling to the bottom of the page shows a sign up page

![image](https://user-images.githubusercontent.com/90155329/137952814-3fcb296e-7b10-4a55-878c-23bdf20ee0d4.png)

As part of the portswigger labs, I get an email client

![image](https://user-images.githubusercontent.com/90155329/137952846-cd7bfe69-ab28-4a0d-a7d6-d6e68975d427.png)

I wonder if I can get multiple coupon codes by signing up multiple times?

![image](https://user-images.githubusercontent.com/90155329/137952869-c14eeb97-4517-4208-a827-9a7f465eb980.png)

I signed up using my email address

![image](https://user-images.githubusercontent.com/90155329/137952899-027c215b-f64d-49ae-994c-23c0b0d4b88c.png)

I received the coupon code of SIGNUP30

![image](https://user-images.githubusercontent.com/90155329/137952919-bd7c0e6d-4437-4740-95ea-7df307e44eae.png)

wiener@exploit-ac821f071f494753c0af41b001ca0006.web-security-academy.net

wiener@bla.exploit-ac821f071f494753c0af41b001ca0006.web-security-academy.net

Added 99 Leather jackets to my cart

![image](https://user-images.githubusercontent.com/90155329/137952953-a600c4d2-7f04-4b4e-89e4-a027b2f157b7.png)

Tested out the coupon 

I lowered the quantity to 1. I wanted to see if the reduction would decrease, and it did.

![image](https://user-images.githubusercontent.com/90155329/137953011-9590e93c-4f1b-4b02-99a8-71ff18ca025b.png)

If the reduction stayed to the same value as having 99 leather jackets, then I would be able to buy the leather jacket for free. 


I went back to the my account page

![image](https://user-images.githubusercontent.com/90155329/137953047-2fcb5454-b7e4-40f8-817e-90291249efad.png)

The gift cards section looks interesting. I entered the SIGNUP30 value. 

![image](https://user-images.githubusercontent.com/90155329/137953089-ced4b388-56d2-43a7-8aa0-7c7b5be7316d.png)

![image](https://user-images.githubusercontent.com/90155329/137953126-082ce49f-711b-4407-8287-9157d0aced89.png)

Received an error of "Invalid gift card"

![image](https://user-images.githubusercontent.com/90155329/137953160-b5175b8c-0cdf-46b3-a059-5b7b6a7b84bd.png)

I wonder if I can get a gift card code by registering with a new email

I registered with the email of wiener@test.exploit-ac821f071f494753c0af41b001ca0006.web-security-academy.net

Registered again

![image](https://user-images.githubusercontent.com/90155329/137953187-2df9287c-2fb9-4c32-a52d-973a65facca5.png)

I did not receive a gift card code in my email

![image](https://user-images.githubusercontent.com/90155329/137953204-1478bab1-0c4e-40ba-b15d-e25dca36278e.png)

I noticed there is a Gift Card item in the shop

![image](https://user-images.githubusercontent.com/90155329/137953237-458f6249-62c4-4126-a906-f6a8089b797c.png)

I purchased this item


![image](https://user-images.githubusercontent.com/90155329/137953269-6aa18f7c-f769-4002-b635-48e3627a2395.png)

![image](https://user-images.githubusercontent.com/90155329/137953290-fd078d58-6b7c-4605-8b00-5e715381b793.png)

This had the code of VEnd45VdUc

I tested this code in the Gift cards section

![image](https://user-images.githubusercontent.com/90155329/137953321-09c77484-8838-4912-b854-aa5728c37e56.png)

![image](https://user-images.githubusercontent.com/90155329/137953358-e22b7033-93aa-4bd2-b9d0-0b82501352dd.png)

I tried the code again, but I received "Invalid gift card"

Will try buying multiple giftcards. As I was doing this, I noticed that by using the SIGNUP30 coupon code, I would only need to spend 98 dollars for 140 dollars worth of gift card. I can then redeem these gift cards and earn about 40$

![image](https://user-images.githubusercontent.com/90155329/137953412-1fe6ea3a-8da2-4441-9f7a-3cd831836c51.png)

I received the following coupon codes

![image](https://user-images.githubusercontent.com/90155329/137953487-2fbd02b9-4bc8-46e3-a953-c0bbd84bddc6.png)

Now, I have to redeem these

![image](https://user-images.githubusercontent.com/90155329/137953507-303b7bcd-2459-4a1d-b55b-6f3388747050.png)

I sent this request to intruder to quickly redeem all of the codes

I chose the Gift-card value as the target

![image](https://user-images.githubusercontent.com/90155329/137953536-3f3484b4-a785-40f1-b390-064c4ee0f1c5.png)

For Payloads, I pasted the coupon code values

![image](https://user-images.githubusercontent.com/90155329/137953570-0c2aa998-9f6d-484b-adda-70a674f33d09.png)

![image](https://user-images.githubusercontent.com/90155329/137953630-23b816f3-a1d2-4f7d-9d23-5829043a6888.png)

Once this is completed, I have 142 store credit. The lab originally started with only 100 store credits.

![image](https://user-images.githubusercontent.com/90155329/137953663-effede5d-cc60-4b3c-b6ab-c56162725eb6.png)

I repeated the process, now that I had more store credit I was able to purchase more gift cards

![image](https://user-images.githubusercontent.com/90155329/137953734-2f590a05-43b7-4fb7-84c0-07ae42479cee.png)

![image](https://user-images.githubusercontent.com/90155329/137953770-eef4c5e3-09f6-4aa9-9d67-92f03589c8e4.png)

I repeated this until I had enough for the leather jacket

During this time, my community burp intruder would take a long time to finnish redeeming the codes. I wrote a python script to redeem the codes faster then intruder

![image](https://user-images.githubusercontent.com/90155329/137953886-bf465ea9-cbdb-464f-a745-40e7fe3da245.png)

![image](https://user-images.githubusercontent.com/90155329/137953914-7d35fad2-3983-4b7b-80d0-34bffda78d87.png)

Eventually, I had enough credit to buy the jacket 

![image](https://user-images.githubusercontent.com/90155329/137953934-69c0167e-033a-4f2e-b3dc-89676dab35ae.png)


![image](https://user-images.githubusercontent.com/90155329/137953981-680d2a64-6dec-4242-9546-9bdae748d942.png)
