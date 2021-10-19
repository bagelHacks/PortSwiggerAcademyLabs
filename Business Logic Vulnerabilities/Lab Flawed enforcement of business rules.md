# Flawed enforcement of business rules

## Objective:

This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".

You can log in to your own account using the following credentials: `wiener:peter`

## Lesson Learned
- Enumerate the whole website. The sign up function was on the bottom of the web page. If this was not discovered, we would not be able to solve this lab. 

----------------------------------------------------


From the landing page, we can see the discount code of NewCust5

![image](https://user-images.githubusercontent.com/90155329/137951537-1c9176c7-1474-4cc6-8709-cc171e84a8cb.png)


From burp, I see the /sign-up link

![image](https://user-images.githubusercontent.com/90155329/137951584-d493280c-d513-4b78-b773-f3e2b8700304.png)

Scrolling to the bottom of the page shows this section

![image](https://user-images.githubusercontent.com/90155329/137951612-b8eec81b-28a1-4b61-903b-ba0abca84f98.png)

To test this function, I need to register my account with an email. 

After I signed in with the credentials of wiener:peter, there is a section to register an email.

![image](https://user-images.githubusercontent.com/90155329/137951655-aa9b8cd7-eae1-4a06-943c-e07624e5eec2.png)

I registered with the email of hacker@hack.com

![image](https://user-images.githubusercontent.com/90155329/137951696-a3a95f32-f647-4cd1-b129-e259a5c8cbf2.png)

![image](https://user-images.githubusercontent.com/90155329/137951803-d3f0edcf-c1c7-4228-96ed-0c2ffd40a515.png)

Next, I signed up using that email

![image](https://user-images.githubusercontent.com/90155329/137951836-9ea6dbb9-98ea-43a9-b1c6-d64aaa309e6a.png)

![image](https://user-images.githubusercontent.com/90155329/137951930-929f117c-037f-4a3d-819a-4dfb06e4b947.png)


After signing up, I was blessed with this coupon code

![image](https://user-images.githubusercontent.com/90155329/137951965-ad5b901a-8b18-4f46-bac8-c2f45b528c4c.png)

SIGNUP30

Next, I added 99 Leather jackets to my cart

![image](https://user-images.githubusercontent.com/90155329/137952024-df4a687b-86e2-4dd8-8429-81d0fcf3c542.png)

It looks like the SIGNUP30 code drops a 30 percentage of the total. 
I will try lowering the quantity of leather jackets to 1. Maybe the application did not account for this and keeps the reduction at $39708.90, even though the quantity of jackets is dropped to just 1 

![image](https://user-images.githubusercontent.com/90155329/137952048-56427c29-e2c3-4825-9619-295de578b615.png)

This did not work, the reduction value also dropped when I dropped the quantity of jackets

![image](https://user-images.githubusercontent.com/90155329/137952082-62046392-51e1-40ac-a09f-b894d7a3ad22.png)

I tried entering the SIGNUP30 code multiple times, but I would receive "coupon already applied"

![image](https://user-images.githubusercontent.com/90155329/137952118-81e5470c-76d8-4606-abe6-9e895e395db6.png)

After testing out the application, I was able to reduce the total to 0.

![image](https://user-images.githubusercontent.com/90155329/137952389-0d9cd214-4b08-4d69-a7b8-e974bc7d23d4.png)


After adding the NEWCUST5 coupon code, I was able to add another SIGNUP30 code. This means that when I add a coupon code, the application only checks the last code added.

![image](https://user-images.githubusercontent.com/90155329/137952428-c9785d41-c20e-43f2-b480-573d54c0e9bf.png)



