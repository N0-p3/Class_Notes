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

Donc, ce qui ce passe concrètement sous le premier commentaire c'est que à partir de `app`, on à accès à plusieurs méthodes qui se trouve à être le nom des requètes (requète GET, POST, PUT, DELETE et etc.) et ces méthodes prennent deux paramètres, en premier l'adresse à laquelle est doit répondre et en deuxième sa job (une fonction ayant `req` et `res` comme paramètres). Ce qui fait que, sous le premier commentaire on dit que si ya une requète GET sur l'adresse `/` on envoie un fichier (avec la fonction `sendFile` de `res`) qui se trouve sur le path suivant `../frontEnd/home.html` (le path vous mettez ce que vous voulez en c'est juste un exemple). <br>

Cependant, sous le deuxième commentaire, on utilise la méthode `use()` qui est une méthode qui fait du "Middleware" et on dit, si jamais tu reçois n'importequoi sur le port que je vais te donner tantôt (dans le `app.listen()`), voici le dossier statique qui représente toutes les requètes qu'un client pourrait faire (`express.static(path)`), arrange toi avec ça. Ce qui est légèrement plus broche à foin mais qui fonctionne tout de même! 

**Note** : la méthode avec gestion d'adresses va faire des beaux URLS et la seconde va faire des laids URLS. <br><br>

Et puis étonnament c'est pomal ça qui est ça. À partir de là vous pouvez faire des API qui réponde au requètes (GET, POST, PUT, DELETE) que vous voulez, lui faire faire ce que vous voulez avec la requète (avec la fonction que vous y donnez) aux adresses que vous voulez (en changeant la route), vous pouvez faire un site web en faisant plusieurs routes qui mène à plusieurs pages vous pouvez mettre un BD en arrière pis faire des shits avec ça. Juste avec ce petit peu d'informations vous pouvez en faire pomal, je voulais juste vous faire remarquer à quel point c'est minuscule et magique MAIS je vais quand même aller plus en détails parce que je vous aime <3 .

**Note 2** : Si vous voulez que votre serveur envoie pas un fichier mais juste une string vous pouvez utilisé la méthode `send()` de l'objet `res` au lieu de `sendFile()`.

## Serveur web (Compacte)

Juste pour les memes je voulais voir jusqu'à quel point je pouvais rétrécir le code pour un serveur web, faque meton que le dossier statique du serveur se trouve à la racine du système, notre serveur ressemblerait à ça (ça fonctionne, je l'ai tester) :

```javascript
const app = require('express')();
app.use(require('express').static('/frontEnd'));
app.listen(8000);
```

# Middleware

Comme expliqué à mainte reprise, du "Middleware" sert à faire une action avant ou après certaines actions prédéfinis d'un "framework". Afin de définir nos fonctions "Middleware" avec Express.js il suffit de passer une fonction en paramètre à `app.use()` (si on veux que le Middleware s'exécute à toutes les types de requètes faites au serveur) ou `app.get()` (si on veux que ça s'exécute juste avec une requète GET, c'est valide pour les autres aussi comme POST, PUT, DELETE et etc.). 

## Exemples d'usage

Par exemple, le "Middleware" suivant s'exécute à toutes les requètes faites :

```javascript
const logger = (req, res, next) => {
    let date = new Date();
    console.log(`A user has made a request for ${req.protocol}://${req.get('host')}${req.originalUrl} on the ${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`);
    next();
}

app.use(logger);
```

Vous remarquerez que `req` et `res` sont des objets super cool qui ont pleins de fonctionnalités amusante, par exemple, dans le code précédant, je vais chercher le protocole (http), l'hôte (localhost:8000) et l'adresse qui est demandé (/api/users).

**Note** : La syntaxe est pédagogique ici, vous pouvez passé la fonction directement à `app.use()`. <br>

Il est aussi possible de faire du Middleware pour une adresse spécifique en précisant la route dans la méthode `app.use()` ou la méthode qui correspond au type de requète auquel vous voulez que le Middleware répond (GET, POST, PUT, DELETE).

```javascript
app.use('api/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```

Vous comprenderez que le Middleware ressemble fortement à la gestion d'une requète à une route prédéterminer à ce point, cependant, à ma compréhension, le Middleware se fait exécuter AVANT que le serveur réponde à la requète.

**Note 2** : Normalement, si on à beaucoup de Middleware, il serait plus "clean" de le placer dans un autre module et de l'importer. <br>

**Note 3** : Pour plus d'information sur le Middleware dans Express.js voyez [le guide d'Express.js sur le Middleware](https://expressjs.com/en/guide/using-middleware.html).

# API

## Read all (avec GET)

Voici un petit exemple de requète API avec Express.js qui va chercher tout les éléments dans une base de donnée MongoDB en utilisant Mongoose et un schéma User :

```javascript
app.get('/api/users', async (req, res) => {
    mongoose.connect('mongodb://localhost/fun');
    try {
        const users = await User.find();
        res.json(users);
    } catch(e) {
        res.json(e.message);
    }
});
```

**Note** : Remarquez que j'utilise `app.get()` vue que une requète qui va chercher tout les infos d'une BD va souvent être une requète GET.

## Read one (avec GET)

Voici un autre exemple de requète API, cette fois-ci nous allons récupérer un seul élément de la BD avec son ID générer automatiquement par MongoDB.

```javascript    
app.get('/api/users/:id', async (req, res) => {
    mongoose.connect('mongodb://localhost/fun');

    const id = (req.params.id.match(/^[0-9a-fA-F]{24}$/) ? mongoose.Types.ObjectId(req.params.id) : 0);

    if (id !== 0) {
        try {
            User.exists({_id: id}, async (err, doc) => {
                if (err || doc == null) {
                    res.status(400).json({message: 'User not found'});
                } else {
                    const user = await User.findOne({_id: id});
                    res.json(user);
                }
            });
        } catch(e) {
            res.json(e.message);
        }
    } else {
        res.status(400).json({message: `id ${req.params.id} is invalid`});
    }
});
```

**NOTE IMPORTANTE** : Ce code semble trop long, je sais mais c'est parce que j'ai gérer chaque erreure, sinon vous pouvez simplement éviter les erreures et faire quelque chose de super simple.

### Explication

Donc, en premier on défini `id` en castant la string que l'on reçoit dans la requète avec `mongoose.Types.ObjectId(req.params.id)` et on à mit ça dans un inline if qui vérifie si l'id reçu dans la requète correspond à un id dont mongoose considère comme valide (sinon y nous pitch une erreure et fait planter le serveur en disant que le cast à pas fonctionner). Si l'id de la requète est pas valide, on met 0 dans `id`. <br>

Ensuite, on vérifie si `id` est pas 0 (comme un peu un guard), si c'est le cas on envoie un status 400 avec un message d'erreur et si c'est pas le cas, finalement, on fait une recherche avec l'id pour voir si il y à un user qui existe à l'id envoyé (puisque un id valide ne veux pas dire un id qui existe). Dans la méthode `User.exists()`, en 1er paramètre on lui passe l'objet de filtre pour trouvé le document auquel cet id appartient et en 2e paramètre on lui passe une fonction async qui à 2 paramètres (`err` représentant une erreure, si il y en à une, et `doc` représentant le document (CONTENANT SEULEMENT L'ID) du document trouvé). <br>

Encore une fois dans un guard on s'assure que si `err` ou `doc` sont `null` on envoie un status 400 avec un message d'erreur et SINON ... finalement... on envoie le document avec `res.json(user);`. <br><br>

**Note** : Remarquez comment on accède à des paramètres GET. Premièrement, on indique le nom du paramètre précédé d'un `:` à son emplacement dans la route. Deuxièmement, on va chercher l'id dans l'objet `req` avec `req.params.id`. Troisièmement il faut le tranformer en objet ObjectId pour mongoose avec `mongoose.Types.ObjectId()`. <br><br>

**Note 2** : Si vous souhaitez changer le status d'une réponse inspectez le else avec vos petit yeux, on change le status avec la fonction `res.status()`, on lui passe le status ET à çela on peux enchainé `.json()` pour envoyer une réponse JSON au client.

## Create one (avec PUT)

Afin de créer un utilisateur avec un API, nous devons utiliser du Middleware préfait dans Express.js pour parser notre requète. Pour ce faire il suffit d'écrire les deux lignes suivante AVANT TOUTES ROUTES dans votre fichier Javascript de serveur :

```javascript
app.use(express.json());
app.use(express.urlencoded({extended: false}));
```

Ensuite créer la route ainsi que son action : 

```javascript
app.post('/api/users', async (req, res) => {
    mongoose.connect('mongodb://localhost/fun');

    const user = new User(req.body);

    await User.create(user);
    res.json({message: 'SUCCES! User created'});
});
```

par la suite, assurez-vous de faire une requète en POST, avec le "Content-Type" à "application/json"  et aussi n'oublier pas d'écrire votre JSON dans le body de votre requète et le tour est joué!

**Note** : Ici je n'ai pas gérer les erreurs... parce que si votre requète est bonne (syntaxiquement) mais que ya trop de stock, mongoose va jeter ce qui à pas dans le schéma (magie) et si ya pas asser de stock, mongoose va juste pas mettre les champs qui sont pas donné par le body de la requète dans le document (MAGIIIIIIIE).

## Delete one (avec DELETE)

AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

# Router

Un router est comme un bon mélange entre un dossier statique et des routes prédéfinis, il devient relativement utile lorsque nous avons plusieurs route sensiblement pareils puisqu'il permet de prendre l'architecture de dossier comme adresse et en plus il permet de relocaliser certaines routes ainsi que leurs actions dans d'autre fichiers ce qui permet de rendre le serveur plus beau et de découper le code de manière élégante. <br><br>

Donc, disons que j'ai le fichier suivant à la racine de mon projet :

```javascript
const express = require('express');
const mongoose = require('mongoose');

const User = require('./schemas/UserSchema');

const PORT = 8000;
const app = express();

app.get('/api/users', async (req, res) => {
    mongoose.connect('mongodb://localhost/fun');
    try {
        const users = await User.find();
        res.json(users);
    } catch(e) {
        res.json(e.message);
    }
});

app.get('/api/users/:id', async (req, res) => {
    mongoose.connect('mongodb://localhost/fun');

    const id = (req.params.id.match(/^[0-9a-fA-F]{24}$/) ? mongoose.Types.ObjectId(req.params.id) : 0);

    if (id !== 0) {
        try {
            User.exists({_id: id}, async (err, doc) => {
                if (err || doc == null) {
                    res.status(400).json({message: 'User not found'});
                } else {
                    const user = await User.findOne({_id: id});
                    res.json(user);
                }
            });
        } catch(e) {
            res.json(e.message);
        }
    } else {
        res.status(400).json({message: 'Invalid Id'});
    }
});

app.listen(PORT);
```

Il serait intelligent de prendre ces deux routes et de les gèrer ailleurs vue qu'elle ont tout deux `/api/users/` en commun. Donc, pour rendre le tout plus clean, on va suivre les étapes suivantes :

1. Faire un path de dossiers qui correspond au path de la route à partir de la racine du projet (dans mon cas, avec : `sudo mkdir api api/users`).
2. Créer un fichier Javascript qui va contenir tout vos routes similaires (dans mon cas, avec : `touch api/users/users.js`).
3. Transférer tout vos routes dans le fichier Javascript que vous venez de faire.
4. Importer Express.js avec : `const express = require('express');`.
5. Initiliser le router avec : `const router = express.Router()`.
6. Importer vos schémas et mongoose (si nécéssaire).
7. Remplacer la référence à `app` pour votre router (dans mon cas, `router`).
8. Remplacer les routes dans vos méthodes (faite comme si vous continuer le path de votre architecture de fichier dans la barre d'addresse).
9. Exporter ce nouveau module dans votre fichier de serveur.
10. Utiliser votre module comme une Middleware avec : `app.use('path/to/route', routerName);`

**Note** : La façon dont vous gérer ou sont vos fichiers et où vont vos routes vous appartient, je ne fait que faire un exemple.<br>

Donc, notre fichier de serveur ressemblerait à ceci maintenant :

```javascript
const express = require('express');
const router = require('./api/users/users');

const PORT = 8000;
const app = express();

app.use('/api/users', router);

app.listen(PORT);
```

Et le fichier dans /api/users ressemblerait à ceci :

```javascript
const express = require('express');
const mongoose = require('mongoose');
const router = express.Router();
const User = require('../../schemas/UserSchema');

router.get('/', async (req, res) => {
    mongoose.connect('mongodb://localhost/fun');
    try {
        const users = await User.find();
        res.json(users);
    } catch(e) {
        res.json(e.message);
    }
});

router.get('/:id', async (req, res) => {
    mongoose.connect('mongodb://localhost/fun');

    const id = (req.params.id.match(/^[0-9a-fA-F]{24}$/) ? mongoose.Types.ObjectId(req.params.id) : 0);

    if (id !== 0) {
        try {
            User.exists({_id: id}, async (err, doc) => {
                if (err || doc == null) {
                    res.status(400).json({message: 'User not found'});
                } else {
                    const user = await User.findOne({_id: id});
                    res.json(user);
                }
            });
        } catch(e) {
            res.json(e.message);
        }
    } else {
        res.status(400).json({message: 'Invalid Id'});
    }
});

module.exports = router;
```

Et voila, libre à vous d'étendre ce router à votre guise!