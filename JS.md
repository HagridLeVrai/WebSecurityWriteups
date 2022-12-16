# Js

## b64js

En parcourant le code source la page, nous avons trouvé ceci:

![image](https://user-images.githubusercontent.com/33731527/208177748-eb4dc21d-06db-4b73-90b9-b656752085f9.png)

On a decode `RXZlckhlYXJkT2ZCYXNlNjQ` de base64 a ascii et on a obtenu le flag. Il a juste fallu rajouter "BFS{}".

## js200

En parcourant le code source la page, nous avons trouvé ceci:

```
var flag = "K@UC,bswslubr.wohp.dibokdmdb";
    var input = document.getElementById("flag").value
input = flag
    var i = 0
    var out = ""
    do {
        out += String.fromCharCode(input.charCodeAt(i) ^ 1);
        out += String.fromCharCode(input.charCodeAt(i + 1) ^ 3);
        out += String.fromCharCode(input.charCodeAt(i + 2) ^ 3);
        out += String.fromCharCode(input.charCodeAt(i + 3) ^ 7);
        i += 4;
    } while (i < 28);

console.log(out)
    if (out === flag) {
        alert("Congratz! Validate this challenge with the flag BFS{" + input + "}")
    } else {
        alert("Try again !")
    }
```

Nous avons executé le code js présent dans l'html en lui donnant comme input `K@UC,bswslubr.wohp.dibokdmdb` ce qui nous a donné le flag ( `JCVD-approves-this-challenge`) le code transforme des int (4) en code ascii (119) et puis en char (q).
