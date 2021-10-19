# Flawed enforcement of business rules

## Objective:

This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

## Lesson Learned
- Enumerate the whole website. The sign up function was on the bottom of the web page. If this was not discovered, we would not be able to solve this lab. 

----------------------------------------------------


From the landing page, we can see the discount code of NewCust5

![[Pasted image 20211006045613.png]]


From burp, I see the /sign-up link

![[Pasted image 20211019093620.png]]

Scrolling to the bottom of the page shows this section

![[Pasted image 20211019093650.png]]

To test this function, I need to register my account with an email. 

After I signed in with the credentials of wiener:peter, there is a section to register an email.

![[Pasted image 20211019093805.png]]

I registered with the email of hacker@hack.com

![[Pasted image 20211019093829.png]]

![[Pasted image 20211019093845.png]]

Next, I signed up using that email

![[Pasted image 20211019093925.png]]

![[Pasted image 20211019093935.png]]


After signing up, I was blessed with this coupon code

![[Pasted image 20211019094050.png]]

SIGNUP30

Next, I added 99 Leather jackets to my cart

![[Pasted image 20211019094344.png]]

It looks like the SIGNUP30 code drops a 30 percentage of the total. 
I will try lowering the quantity of leather jackets to 1. Maybe the application did not account for this and keeps the reduction at $39708.90, even though the quantity of jackets is dropped to just 1 

![[Pasted image 20211019094507.png]]

This did not work, the reduction value also dropped when I dropped the quantity of jackets

![[Pasted image 20211019094722.png]]

I tried entering the SIGNUP30 code multiple times, but I would receive "coupon already applied"

![[Pasted image 20211019095520.png]]

After testing out the application, I was able to reduce the total to 0.

![[Pasted image 20211019095415.png]]

After adding the NEWCUST5 coupon code, I was able to add another SIGNUP30 code. This means that when I add a coupon code, the application only checks the last code added.

![[Pasted image 20211019100102.png]]



