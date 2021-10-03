# Lab Excessive trust in client-side controls

## Objective:
This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

This is what the landing page looks like 

![[Pasted image 20211003020757.png]]

The objective is to but the following product

![[Pasted image 20211003020832.png]]

I clicked on this product, then I clicked "Add to cart"

![[Pasted image 20211003020908.png]]

From my cart, I can see that this costs 1337 dollars

![[Pasted image 20211003020946.png]]

I will click "place order" and intercept the request with  Burp Intercept 

I received and error of "not logged in"

![[Pasted image 20211003021109.png]]

I logged in with the credentials of wiener:peter 

![[Pasted image 20211003021233.png]]

After logging in, I placed the order and intercepted the request 

![[Pasted image 20211003021331.png]]
I received an error of "insufficient funds"

![[Pasted image 20211003021435.png]]

I went back and intercepted the request when I added the item to my cart

![[Pasted image 20211003021816.png]]

![[Pasted image 20211003021906.png]]

I noticed that the price is part of the post request. 

I modified the price to 1

![[Pasted image 20211003022237.png]]

Now when I visit my cart, it has a price of 0.01

![[Pasted image 20211003022256.png]]

Clicking purchase completed the lab 

![[Pasted image 20211003022312.png]]