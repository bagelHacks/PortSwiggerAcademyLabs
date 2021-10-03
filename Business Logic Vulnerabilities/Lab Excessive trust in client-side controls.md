# Lab Excessive trust in client-side controls

## Objective:
This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

This is what the landing page looks like 

![image](https://user-images.githubusercontent.com/90155329/135768457-5308af34-d9f7-430f-ad04-5a56c9bc6f67.png)

The objective is to but the following product

![image](https://user-images.githubusercontent.com/90155329/135768460-ae4f44b3-917f-4251-9c08-443d486484f3.png)

I clicked on this product, then I clicked "Add to cart"

![image](https://user-images.githubusercontent.com/90155329/135768469-e08eb356-224c-4201-a5a7-e02b20568996.png)

From my cart, I can see that this costs 1337 dollars

![image](https://user-images.githubusercontent.com/90155329/135768479-2df8a0b1-cd68-4fc6-83d5-5a864ea19a88.png)

I will click "place order" and intercept the request with  Burp Intercept 

I received and error of "not logged in"

![image](https://user-images.githubusercontent.com/90155329/135768485-b634d144-e4f2-42a4-8cd3-be5c00ab1c5f.png)

I logged in with the credentials of wiener:peter 

![image](https://user-images.githubusercontent.com/90155329/135768488-81584af1-7efd-4e7f-9540-4233c742344b.png)

After logging in, I placed the order and intercepted the request 

![image](https://user-images.githubusercontent.com/90155329/135768500-569002e8-0aa6-4352-8fb6-be8127b42b8d.png)
I received an error of "insufficient funds"

![image](https://user-images.githubusercontent.com/90155329/135768504-4ef62eef-b106-499d-8594-b9ef98921851.png)

I went back and intercepted the request when I added the item to my cart

![image](https://user-images.githubusercontent.com/90155329/135768517-84363f4c-851e-4a5a-bc7f-8d014304a9ab.png)

![image](https://user-images.githubusercontent.com/90155329/135768522-68a2a034-f8d1-459f-893c-358c618cbd97.png)

I noticed that the price is part of the post request. 

I modified the price to 1

![image](https://user-images.githubusercontent.com/90155329/135768535-5d1e19da-f682-4663-b67c-00daa7e54d55.png)

Now when I visit my cart, it has a price of 0.01

![image](https://user-images.githubusercontent.com/90155329/135768543-56f802a1-579a-4031-a433-74f1fedbe2e2.png)

Clicking purchase completed the lab 

![image](https://user-images.githubusercontent.com/90155329/135768548-417be5b5-e7db-4bb4-9f78-0147cd88abc4.png)
