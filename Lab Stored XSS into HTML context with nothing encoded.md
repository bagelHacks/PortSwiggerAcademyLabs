# Lab Stored XSS into HTML context with nothing encoded

## Objective:

 This lab contains a stored cross-site scripting vulnerability in the comment functionality.

To solve this lab, submit a comment that calls the alert function when the blog post is viewed. 

This is what the landing page looks like:

![image](https://user-images.githubusercontent.com/90155329/132959828-2743b335-4a83-452a-899b-2f1c8979fdbd.png)
Clicking on one of the posts, I can see the comment section.

![image](https://user-images.githubusercontent.com/90155329/132959833-d4214d8e-3c3a-4d0a-9070-181c53f5b681.png)

From the PortSwigger CheatSheet, I copied the following payload

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

![image](https://user-images.githubusercontent.com/90155329/132959846-e86f80d1-3bf6-4fb6-a3fe-7b0f01ceb504.png)

`<xss onafterscriptexecute=alert(1)><script>1</script>`

I posted the payload into the blog page.

![image](https://user-images.githubusercontent.com/90155329/132959848-4791f3d7-6997-4c9d-94bb-35d0ca918035.png)

If the website stores this payload, then any user who visits this page will execute the javascript which would generate an alert popup.

After posting the payload, I reloaded the page and received an alert popup.

![image](https://user-images.githubusercontent.com/90155329/132959855-63b73773-7a5b-41be-a282-e104c2736e81.png)
