
  

#  SSRF 


### SSRF1
On the page https://ssrf1.secu-web.blackfoot.dev/ we can see in the session, a "GOSESSION" property.
If we go to https://ssrf1.secu-web.blackfoot.dev/secret without the cookie token.
We have the response 
```{"ok":false,"message":"Missing GOSESSION ... You are not connected... get away !","flag":""}```.
By searching on google the weird message "Missing GOSESSION"
https://www.google.com/search?q=%22Missing+GOSESSION%22&oq=%22Missing+GOSESSION%22&aqs=chrome..69i57.602j0j4&sourceid=chrome&ie=UTF-8
https://www.synacktiv.com/en/publications/fic2020-prequals-ctf-write-up.html
I found a ctf website who explain how to use the vulnerability.
By adding "%20HTTP/1.1%0ACookie:GOSESSION=" and say specifically go to the secret page from localhost, we get a JWT token and by simply adding it to JWT.io we get the flag.
https://ssrf1.secu-web.blackfoot.dev/host?host=localhost/secret?xx=xx%20HTTP/1.1%0ACookie:GOSESSION=

