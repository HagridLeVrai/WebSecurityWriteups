# Wordstress

Le site est un `Wordpress` en version `4.2.34`.

Nous avons trouvé un [exploit](https://www.exploit-db.com/exploits/36844) compatible avec cette version.

Si le texte du commentaire est suffisamment long, il sera tronqué lors de son insertion dans la base de données. La limite de taille du type TEXT de MySQL est de 64 kilo-octets.

La troncature entraîne la génération d'un HTML malformé sur la page. 

L'attaquant peut fournir n'importe quel attribut dans les balises HTML autorisées, et donc exploiter des vulnérabilités XSS.

```
<a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'></a>
```

Je pensais pouvoir affecter l'admin lors du visionnage d'un des messages infectés mais je n'ai pas réussi à mettre en place l'exploit.
