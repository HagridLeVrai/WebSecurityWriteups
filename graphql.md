# Confessions

Lors de ce challenge, nous devions récupérer un message écris plus tôt par un autre utilisateur.

A chaque nouvelle lettre entrée dans le champs `Message`, une requête `addConfession`(qui ajoute une confession) et `confession`(qui get une confession avec un hash) sont effectués.

La config du serveur graphql et ses routes a été récupérer et nous avons exploré ses routes.

![image2](https://user-images.githubusercontent.com/33731527/208184872-23c4d7aa-0784-4ab4-a306-63cb5c83d1fd.png)

Nous avons trouvé une route `RequestLog`: 
```
{
  "name": "requestsLog",
  "description": "Show the resolver access log. TODO: remove before production release",
  "args": [],
  "type": {
    "kind": "LIST",
    "name": null,
    "ofType": {
      "kind": "OBJECT",
      "name": "Access",
      "ofType": null
  }
  },
  "isDeprecated": false,
  "deprecationReason": null
},
```
Cette route permet de récuperer tous les logs.

![image3](https://user-images.githubusercontent.com/33731527/208184596-121e0d3b-21f3-4176-b5c8-2432c665c1eb.png)

Grâce à celà nous avons pu récupérer le hash du message à chaque nouvelle lettre. 

Puisqu'un hash est généré à chaque nouvelle lettre, le sha256 peut être reproduit.

![image](https://user-images.githubusercontent.com/33731527/208184986-a9ff6243-2ac7-4e71-9277-668cbf32223a.png)

Le flag a été retrouvé en créant un script Python qui testait le hash d'une phrase, caractère par caractère, en ajoutant tous les caractère ascii possible et les comparait au hashs des logs.
Si c'est le même hash alors c'est le bon caractère.
