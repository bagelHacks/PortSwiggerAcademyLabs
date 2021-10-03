# Lab High-level logic vulnerability

Objective: 

This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

---------------------------------------------------------------

This is what the landing page looks like 

![image](https://user-images.githubusercontent.com/90155329/135768619-aab36ca9-f05d-4f7b-87e2-dc322200912a.png)

I logged in with the credentials of wiener:peter

I added the "Lightweight "l33t" Leather Jacket to my cart and intercepted the request

![image](https://user-images.githubusercontent.com/90155329/135768628-6ed12003-1eb9-4dc7-939b-9cf81201a965.png)

![image](https://user-images.githubusercontent.com/90155329/135768633-bfbc8861-e7ab-4c07-acd5-85c8b6e283b1.png)

From the post request, there does not seem like a way to modify the jacket money value. 

After I added it to my cart, I clicked "purchase" and intercepted the request

![image](https://user-images.githubusercontent.com/90155329/135768644-5b33dc52-d93f-468e-8cbd-6479c0462258.png)

![image](https://user-images.githubusercontent.com/90155329/135768650-94887d37-c8e9-483c-99f6-52e5ee47a999.png)

I went back and added the jacket to my cart again

![image](https://user-images.githubusercontent.com/90155329/135768654-99dba898-ce5f-4220-9872-3bed6f2750ec.png)

![image](https://user-images.githubusercontent.com/90155329/135768661-f03d3a9d-2f42-434e-9442-5a2a8e01fb74.png)

I wonder what would happen if I placed a -1 for the quantity value 

![image](https://user-images.githubusercontent.com/90155329/135768666-cf7c9e6b-cc9e-48b2-a613-4e683edafe5a.png)

Now, from the cart, the value of the Leather Jacket is -1337

![image](https://user-images.githubusercontent.com/90155329/135768681-b3c64f7c-10fb-411f-a780-971aae0a2d7e.png)

This time I received an error, "Cart total price cannot be less than zero"

![image](https://user-images.githubusercontent.com/90155329/135768690-17725dfb-3de1-4428-9334-507176455d47.png)

I wonder if I can add other products to make the cost greater then 0 

I will add this Burp Protection product 

![image](https://user-images.githubusercontent.com/90155329/135768696-df4c9c80-2a7c-42a6-a442-2ea470bc4c96.png)

![image](https://user-images.githubusercontent.com/90155329/135768701-50a96bb8-34c6-4002-b36e-0718b4875047.png)

If I add 14, this would cost about 1,300. 

Now, Since I had a negative jacket (-1337) + 14 Burp protections (+1,400), the total cost is 60.20

![image](https://user-images.githubusercontent.com/90155329/135768712-3472b70c-cc6b-4bcd-96bd-4f4a8028609e.png)

Placing the order was successful, however the lab was not completed

![image](https://user-images.githubusercontent.com/90155329/135768723-64bc21cf-df81-4f9b-98f1-5430431a038d.png)

This is probably because quantity of the Jacket is -1.
I need to change the cart so that the Jacket is 1, and the other items are negative 

![image](https://user-images.githubusercontent.com/90155329/135768738-d1ec537e-b22e-43de-8ff4-1e8c44758bc1.png)

Placing my order completed the lab 

![image](https://user-images.githubusercontent.com/90155329/135768743-5f0705b5-b23e-4b6d-b125-ae9b9f282124.png)

