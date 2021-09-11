# Lab Stored XSS into HTML context with nothing encoded

## Objective:

 This lab contains a stored cross-site scripting vulnerability in the comment functionality.

To solve this lab, submit a comment that calls the alert function when the blog post is viewed. 

This is what the landing page looks like:

![[Pasted image 20210911153845.png]]

Clicking on one of the posts, I can see the comment section.

![[Pasted image 20210911153918.png]]

From the PortSwigger CheatSheet, I copied the following payload

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

![[Pasted image 20210911154009.png]]

`<xss onafterscriptexecute=alert(1)><script>1</script>`

I posted the payload into the blog page.

![[Pasted image 20210911154037.png]]

If the website stores this payload, then any user who visits this page will execute the javascript which would generate an alert popup.

After posting the payload, I reloaded the page and received an alert popup.

![[Pasted image 20210911154140.png]]
