# Auth

## Auth50

En inspectant le code source de la page,

```
if (isset($_POST['username']) && isset($_POST['password']))
{
    $username = htmlspecialchars(trim($_POST['username']));
    $password = htmlspecialchars(trim($_POST['password']));
    if (!empty($username) && !empty($password)) {
        if ($username === $g_username) {
            if ($password === $g_password) {
                $message = "Congratz for this great guessing challenge ! $g_flag";
            } else $message = "At least you got the username  ( $g_username )";
        } else $message = 'You are far away from the flag !';
    }
}
```

J'ai vu que si l'on met le bon username, il nous prévient que c'est le bon. J'ai alors testé admin par reflex et c'était le bon username. J'ai alors essayé password pour le mot de passe et ça a fonctionné.

## Auth100

En inspectant le code source de la page,

```
if (isset($_POST['username']) && isset($_POST['password']))
{
    $username = htmlspecialchars(trim($_POST['username']));
    $password = htmlspecialchars(trim($_POST['password']));
    if (!empty($username) && !empty($password) && strlen($username) > 5)
    {
        $sum = 0;
        for ($i = 0 ; $i < strlen($username) ; ++$i)
            $sum += ord($username[$i]); // 1nTr3sT1nG, 15n't 1t ?
        if ($password === strval($sum)) {
            $message = 'Congrats ! Validate with this flag : '.$g_flag;
        } else $message = 'Bad Password ! Remember that the password is generated with the username ! Like a KeygenMe !';
    } else $message = "Username have to be 6 chars at least";
}
```

Le code PHP de la page convertissait chaque caractère du `username` en code ascii et les additionnais, puis vérifiais que cette somme était égale au mot de passe renseigné.

Nous avons donc repris ce code et constaté que cette somme était égale à `837` pour le mot `1nTr3sT1nG`.

```
console.log("1nTr3sT1nG".charCodeAt(0))
console.log("1nTr3sT1nG".charCodeAt(1))
console.log("1nTr3sT1nG".charCodeAt(2))
console.log("1nTr3sT1nG".charCodeAt(3))
console.log("1nTr3sT1nG".charCodeAt(4))
console.log("1nTr3sT1nG".charCodeAt(5))
console.log("1nTr3sT1nG".charCodeAt(6))
console.log("1nTr3sT1nG".charCodeAt(7))
console.log("1nTr3sT1nG".charCodeAt(8))
console.log("1nTr3sT1nG".charCodeAt(9))
console.log("1nTr3sT1nG".charCodeAt(10))
49+110+84+114+51+115+84+49+110+71
837
```

Cela nous a donné le mot de passe afin d'obtenir le flag.

## Auth200

En inspectant le code source de la page, nous avons constaté que le script fait un `XOR` de l'input utilisateur avec une clé `dTh1s_1s_@_x0r_k3y_l0l!` et vérifie si le résultat est égal à `3c094317451c232d195319026c1e2a09431f7e38075d527e1052`.

```
$encrypted_flag .= chr(ord($flag[$i]) ^ ord($key[$i % strlen($key)]));
```

Nous avons donc reverse le XOR avec notre scipt en python en faisant `3c094317451c232d195319026c1e2a09431f7e38075d527e1052` XOR de `Th1s_1s_@_x0r_k3y_l0l!` pour obtenir l'input nécessaire.

![image](https://user-images.githubusercontent.com/33731527/208175082-d2b571ee-d1f6-4cc3-86b7-0395f597e573.png)

Nous avons donc obtenu `hard_to_crack_i_guess_lol!!!!`. En rentrant ceci dans le site et nous avons obtenu le flag.
