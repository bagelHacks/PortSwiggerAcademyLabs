# Lab Low-level logic flaw

## Objective:

This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

This is what the landing page looks like 

![image](https://user-images.githubusercontent.com/90155329/135768892-4bf68eb8-2c5c-4f23-9221-0771bce04d42.png)

I logged in with the credentials of wiener:peter

I started by adding the "Lightweight "l33t" Leather Jacket" to my cart and intercepting the request

![image](https://user-images.githubusercontent.com/90155329/135768900-3d9f1070-ad4b-4e95-847a-5a0d4924e302.png)

![image](https://user-images.githubusercontent.com/90155329/135768903-62550966-2f7d-46d0-bf6c-44c3a04aa8be.png)

I changed the value of quantity to -1 

![image](https://user-images.githubusercontent.com/90155329/135768911-a8c00d58-ce61-4180-9108-bde97446df59.png)

I kept playing with the values and was unable to lower the base price of 1337 this way. 

Eventually I looked at the answer. The vulnerability in this web application is a flaw in the quantity field. When this number is too high, then the total becomes a negative number. 

I used intruder to repeatedly add 99 "Lightweight "l33t" Leather Jackets" to my cart

![image](https://user-images.githubusercontent.com/90155329/135768916-f851120b-73b2-40fb-b129-aead83ec8220.png)

![image](https://user-images.githubusercontent.com/90155329/135768928-0d7f071c-f3d1-408c-9ea4-7d1365eede72.png)

With the above configured, the attack just kept adding 99 of the jacket values

![image](https://user-images.githubusercontent.com/90155329/135768936-e311b2fd-b990-470e-b017-0223d604a17a.png)

Eventually, from the cart, the total became a negative number. This is because it the application could not handle such a large quantity value. 

![image](https://user-images.githubusercontent.com/90155329/135768946-8c0195e6-3e65-4490-bb29-554febb52fca.png)


I tried to purchase, but received error "Cart total price cannot be less than zero"

![image](https://user-images.githubusercontent.com/90155329/135768951-6a317501-309c-4c48-8156-8b10d1701cbe.png)

This means I need to add values in the cart until the total is positive 

I chose the "hologram Stand in" item which costs 91.95

![image](https://user-images.githubusercontent.com/90155329/135768959-0d6ee84d-eb66-4bea-b88f-298cac0473d7.png)

Right now the total is -6347662.02 , which means I will need 69033 "hologram Stand in" items to bring the total back to positive (69033 x 91.95) - 6347662. = 78

I used intruder to add 6347662 "Hologram Stand in" items to the cart 

![image](https://user-images.githubusercontent.com/90155329/135768973-06862bd8-1963-4390-acb2-2c541ae78a12.png)

![image](https://user-images.githubusercontent.com/90155329/135768980-0286a24c-e6ab-4525-8bed-9ccb0af5890d.png)

Eventually the number goes back to positive

![image](https://user-images.githubusercontent.com/90155329/135768986-346146d6-f33d-4c55-9f1f-187ff5f44ebd.png)

Placing the order solved the lab

![image](https://user-images.githubusercontent.com/90155329/135768994-68a43af1-cf31-4608-a1ad-55c6a53779d9.png)
