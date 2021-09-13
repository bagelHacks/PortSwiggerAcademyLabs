# Lab Reflected XSS with some SVG markup allowed

 This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some SVG tags and events.

To solve the lab, perform a cross-site scripting attack that calls the alert() function. 

## 1. Determine what tags are allowed 

I used the following simple payload

<script>alert(1)</script>

![[Pasted image 20210913084852.png]]

Next, I intercepted it with burp proxy, and sent it to intruder 

![[Pasted image 20210913084938.png]]


Picked "Battering Ram" and the "alert" string as the target 

![[Pasted image 20210913085003.png]]


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

![[Pasted image 20210913085539.png]]

## 2. Pick the payload

Since we know that animate transform and svg are working tags, I picked the payload from the XSS cheat sheet

![[Pasted image 20210913091543.png]]

`<svg><animatetransform onbegin=alert(1) attributeName=transform>`
	
![[Pasted image 20210913091554.png]]
	
This resulted in successful XSS
	
![[Pasted image 20210913091623.png]]