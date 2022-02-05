# Serveur web

Voici le "boilerplate code" pour un serveur web, dans les explications, j'expliquerai ce qui se passe et comment on peux batir là dessus. Voici l'exemple :

```javascript
const express = require('express');
const path = require('path');

const PORT = 8000;
const app = express();

// Avec gestion d'adresses
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, '..', 'frontEnd', 'home.html'))
}); 

// Avec un dossier statique
app.use(express.static(path.join(__dirname, '..', 'frontEnd')));

app.listen(PORT, () => console.log(`Server started on ${PORT}`));
```

## Explications

1. On importe Express.js et initialise l'application en plus du port avec les première lignes : 

```javascript
const express = require('express');
const path = require('path');

const PORT = 8000;
const app = express();
```

2. Les quelques lignes sous les commentaires font la même chose, la première utilise des adresses écrite manuellement (donc en gros on se fait une route) et la seconde utilise un dossier sur lequel Express.js va se baser (au niveau de l'architecture des fichiers) pour gérer les requètes (au lieu de préciser l'adresse pour chaque page).

```javascript
// Avec gestion d'adresses
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, '..', 'frontEnd', 'home.html'))
}); 

// Avec un dossier statique
app.use(express.static(path.join(__dirname, '..', 'frontEnd')));
```

3. Finalement, on écoute sur le port pour servir les clients (la fonctions flèche-anonyme est optionnel).

```javascript
app.listen(PORT, () => console.log(`Server started on ${PORT}`));
```

Donc, ce qui ce passe concrètement sous le premier commentaire c'est que à partir de `app`, on à accès à plusieurs méthodes qui se trouve à être le nom des requètes (requète GET, POST, PUT, DELETE et etc.) et ces méthodes prennent deux paramètres, en premier l'adresse à laquelle est doit répondre et en deuxième sa job (une fonction ayant `req` et `res` comme paramètres). Ce qui fait que, sous le premier commentaire on dit que si ya une requète GET sur l'adresse `/` on envoie un fichier (avec la fonction `sendFile` de `res`) qui se trouve sur le path suivant `../frontEnd/home.html` (le path vous mettez ce que vous voulez en c'est juste un exemple). <br><br>

Cependant, sous le deuxième commentaire, on utilise la méthode `use()` qui est une méthode qui fait du "Middleware" et on dit, si jamais tu reçois n'importequoi sur le port que je vais te donner tantôt (dans le `app.listen()`), voici le dossier statique qui représente toutes les requètes qu'un client pourrait faire (`express.static(path)`), arrange toi avec ça. Ce qui est légèrement plus broche à foin mais qui fonctionne tout de même! 

**Note** : la méthode avec gestion d'adresses va faire des beaux URLS et la seconde va faire des laids URLS. <br><br>

Et puis étonnament c'est pomal ça qui est ça. À partir de là vous pouvez faire des API qui réponde au requètes (GET, POST, PUT, DELETE) que vous voulez, lui faire faire ce que vous voulez avec la requète (avec la fonction que vous y donnez) aux adresses que vous voulez (en changeant la route), vous pouvez faire un site web en faisant plusieurs routes qui mène à plusieurs pages vous pouvez mettre un BD en arrière pis faire des shits avec ça. Juste avec ce petit peu d'informations vous pouvez en faire pomal, je voulais juste vous faire remarquer à quel point c'est minuscule et magique MAIS je vais quand même aller plus en détails parce que je vous aime <3 .

## Serveur web (Compacte)

Juste pour les memes je voulais voir jusqu'à quel point je pouvais rétrécir le code pour un serveur web, faque meton que le dossier statique du serveur se trouve à la racine du système, notre serveur ressemblerait à ça (ça fonctionne, je l'ai tester) :

```javascript
const app = require('express')();
app.use(require('express').static('/frontEnd'));
app.listen(8000);
```