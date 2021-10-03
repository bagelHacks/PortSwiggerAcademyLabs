# Lab High-level logic vulnerability

Objective: 

This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

---------------------------------------------------------------

This is what the landing page looks like 

![[Pasted image 20211003023525.png]]

I logged in with the credentials of wiener:peter

I added the "Lightweight "l33t" Leather Jacket to my cart and intercepted the request

![[Pasted image 20211003024331.png]]

![[Pasted image 20211003024348.png]]

From the post request, there does not seem like a way to modify the jacket money value. 

After I added it to my cart, I clicked "purchase" and intercepted the request

![[Pasted image 20211003024534.png]]

![[Pasted image 20211003024556.png]]

I went back and added the jacket to my cart again

![[Pasted image 20211003024714.png]]

![[Pasted image 20211003024708.png]]

I wonder what would happen if I placed a -1 for the quantity value 

![[Pasted image 20211003024749.png]]

Now, from the cart, the value of the Leather Jacket is -1337

![[Pasted image 20211003024827.png]]

This time I received an error, "Cart total price cannot be less than zero"

![[Pasted image 20211003025054.png]]

I wonder if I can add other products to make the cost greater then 0 

I will add this Burp Protection product 

![[Pasted image 20211003025928.png]]

![[Pasted image 20211003030148.png]]

If I add 14, this would cost about 1,300. 

Now, Since I had a negative jacket (-1337) + 14 Burp protections (+1,400), the total cost is 60.20

![[Pasted image 20211003030231.png]]

Placing the order was successful, however the lab was not completed

![[Pasted image 20211003030316.png]]

This is probably because quantity of the Jacket is -1.
I need to change the cart so that the Jacket is 1, and the other items are negative 

![[Pasted image 20211003030629.png]]

Placing my order completed the lab 

![[Pasted image 20211003030653.png]]

