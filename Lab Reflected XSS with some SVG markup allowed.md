# Lab Reflected XSS with some SVG markup allowed

 This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some SVG tags and events.

To solve the lab, perform a cross-site scripting attack that calls the alert() function. 

## 1. Determine what tags are allowed 

I used the following simple payload

`<script>alert(1)</script>`

![image](https://user-images.githubusercontent.com/90155329/133090658-72bd475c-493f-4c01-85e9-42353e561667.png)

Next, I intercepted it with burp proxy, and sent it to intruder 

![image](https://user-images.githubusercontent.com/90155329/133090671-227dfc6e-2e97-4214-8651-2b588b370229.png)


Picked "Battering Ram" and the "alert" string as the target 

![image](https://user-images.githubusercontent.com/90155329/133090707-d8602fb8-0a7c-4683-817e-02d2988175da.png)


Pasted tags payload from XSS cheat sheet and started the attack 

The following tags were accepted 

animatetransform
image
svg
title

## What is SVG File

Scalable Vector Graphics (SVG) is an XML-based vector image format for two-dimensional graphichs with support for interactivity and animation. 

![[Pasted image 20210913085453.png]]

http://ghostlulz.com/xss-svg/

SVG files also support inline javascript code. 

![image](https://user-images.githubusercontent.com/90155329/133090731-5d711a41-11a4-4853-994e-9cb5a38911cb.png)

## 2. Pick the payload

Since we know that animate transform and svg are working tags, I picked the payload from the XSS cheat sheet

![image](https://user-images.githubusercontent.com/90155329/133090773-ed473ef1-3362-46db-afa5-1387514b2c16.png)

`<svg><animatetransform onbegin=alert(1) attributeName=transform>`
	
![image](https://user-images.githubusercontent.com/90155329/133090789-acc0c70b-0f13-4012-bc44-3dec4fe6ace5.png)
	
This resulted in successful XSS
	
![image](https://user-images.githubusercontent.com/90155329/133090827-8788e33b-9ea3-466b-b5f8-c817d16e5fd6.png)
