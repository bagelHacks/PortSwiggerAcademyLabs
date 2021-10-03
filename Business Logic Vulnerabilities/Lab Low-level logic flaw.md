# Lab Low-level logic flaw

## Objective:

This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

This is what the landing page looks like 


![[Pasted image 20211003032910.png]]

I logged in with the credentials of wiener:peter

I started by adding the "Lightweight "l33t" Leather Jacket" to my cart and intercepting the request

![[Pasted image 20211003033037.png]]

![[Pasted image 20211003033021.png]]

I changed the value of quantity to -1 

![[Pasted image 20211003033059.png]]

I kept playing with the values and was unable to lower the base price of 1337 this way. 

Eventually I looked at the answer. The vulnerability in this web application is a flaw in the quantity field. When this number is too high, then the total becomes a negative number. 

I used intruder to repeatedly add 99 "Lightweight "l33t" Leather Jackets" to my cart

![[Pasted image 20211003041753.png]]

![[Pasted image 20211003041803.png]]

With the above configured, the attack just kept adding 99 of the jacket values

![[Pasted image 20211003041835.png]]

Eventually, from the cart, the total became a negative number. This is because it the application could not handle such a large quantity value. 

![[Pasted image 20211003041849.png]]


I tried to purchase, but received error "Cart total price cannot be less than zero"

![[Pasted image 20211003041941.png]]

This means I need to add values in the cart until the total is positive 

I chose the "hologram Stand in" item which costs 91.95

![[Pasted image 20211003042846.png]]

Right now the total is -6347662.02 , which means I will need 69033 "hologram Stand in" items to bring the total back to positive (69033 x 91.95) - 6347662. = 78

I used intruder to add 6347662 "Hologram Stand in" items to the cart 

![[Pasted image 20211003042932.png]]

![[Pasted image 20211003042941.png]]

Eventually the number goes back to positive

![[Pasted image 20211003043734.png]]

Placing the order solved the lab

![[Pasted image 20211003043829.png]]