# Connexion

Afin de se connecté à votre base de donné MongoDB avec Node.js, assurez-vous d'avoir suivis les étapes dans l'[installation](./Theorie.md#installation) et inspirez vous du code boilerplate suivant (libre de droit) dans votre fichier javascript :

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/testdb');
```

Alternativement, il est possible de lancer une fonction lors de la connexion et de gérer les erreures à la connexion en passant deux fonctions à la méthode `connect()`, la première est une fonction sans paramètres qui est exécuté à chaque connexion et la seconde est une connexion qui reçoit un paramètre (l'erreure) et est exéctuer à chaque erreure de connexion. Le code boilerplate ressemble à ceci : 

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/testdb', () => {
    console.log('Connexion détectée!\n');
}, (e) => {
    console.log(`Erreure de connexion : ${e}`)
});
```

Cependant, mongoose est tellement magique que même si vous tentez d'exécuter des commandes et qu'aucune connexion n'à été faite, il va les mettre dans une file et les exécuter lorsqu'une connexion est finalement ouverte (stu pas magique!). Ce qui rend la seconde manière de se connecter un peu désuette.

# Schéma

## Définition

Un schéma est une définition d'une collection. En gros, vue que MongoDB permet de mettre des documents ayant une structure différente dans une même collection, mongoose "patch" ça avec ce qu'on appel des schémas. Ces schéma ne vont non seulement définir la structure de nos collections mais aussi, par le fait même définir la structure de nos objets (documents ou modèles) qui seront envoyés à notre base de donné.

## Création d'un schéma

Afin de créer un schéma, nous devons faire un fichier javascript qui va contenir notre schéma et s'assurer que mongoose y est importé, ensuite il suffira de mettre ce schéma dans une variable et de définir notre schéma avec des paires clef-type (comme les documents dans MongoDB) séparer par une virgule. Ensuite, il faudra créer un modèle de ce schéma. Pour ce faire, nous allons utilisé la méthode `model()` de mongoose en lui passant le nom du schéma ainsi que le schéma que nous avons stocker dans une variable précédement. Pour terminer il ne restera plus qu'à exporter le modèle. Le code ressemblera essentiellement à ceci : 

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    name: String,
    age: Number
});

module.exports = mongoose.model('User', userSchema);
```

**Note** : Les types de mongoose sont disponibles [ici](https://mongoosejs.com/docs/schematypes.html).

## Utilisation d'un schéma

Afin d'utiliser un schéma, il suffit de l'importer et de s'en servir pour créer des objets : 

```javascript
const mongoose = require('mongoose');
const User = require('./User'); //Importation

mongoose.connect('mongodb://localhost/testdb');

const user = new User({name: 'Bob', age: 2}); //Utilisation
```

**Note 2** : Remarquez qu'appartir de `User`, nous avons non seulement un modèle mais aussi la collection `users` dans notre base de donnée, puisque à partir de `User`, nous avons toutes les fonctions (de mongosh) comme `find()`, `findOne()` et etc.

## Architecture de schéma

Dans un schéma, les données peuvent être architecturées vraiment comme on le souhaite. On peux avoir des reférences à d'autres modèles (un peu comme des clefs secondaires), on peux avoir des tableaux de données, bref tout ce que vous avez vue qu'on peux faire avec mongosh on peux le faire avec mongoose mais en mieux! (c'est plus "clean" avec les schémas). En voici un exemple : 

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    name: String,
    age: Number,
    hobbies: [String],
    birthday: Date,
    bestFriend: mongoose.SchemaTypes.ObjectId,
    favoriteThings: [],
    address: {
        zipCode: String,
        number: Number,
        street: String,
        city: String
    }
});

module.exports = mongoose.model('User', userSchema);
```

Maintenant dans notre schéma `User` nous avons un tableau typé (`hobbies`), un tableau non typé qui peux contenir tout types confondues (`favoriteThings`), une date (`birthday`), une référence à un autre modèle (`bestFriend`) et un autre schéma (`address`)!<br><br>
Cependant, il serait plus propre de prendre notre objet `address` et de la mettre dans son propre schéma (et idéalement dans son propre fichier)! Ainsi :

```javascript
const mongoose = require('mongoose');

const addressSchema = new mongoose.Schema({
    zipCode: String,
    number: Number,
    street: String,
    city: String
});

const userSchema = new mongoose.Schema({
    name: String,
    age: Number,
    hobbies: [String],
    birthday: Date,
    bestFriend: mongoose.SchemaTypes.ObjectId,
    favoriteThings: [],
    address: addressSchema
});

module.exports = mongoose.model('User', userSchema);
```

**Note** : Ainsi (en mettant l'addresse dans un autre schéma), mongoDB va créer une clef pour cet objet en plus des données fourni à l'intérieur. Un peu comme si l'addresse était une chose à part et donc qu'elle avait sa propre identité à part.<br><br>
Pour ce qui est de travailler avec ce schéma c'est comme avant sauf qu'il y à maintenant plus de données dans votre modèle à créer et chacun d'entre eux doit contenir le bon type. <br>
**Note 2** : Si vous voulez spécifier que le champ `bestFriend` est un `User` aussi, vous pouvez étendre la définition de ce champ ainsi :

```javascript
const userSchema = new mongoose.Schema({
    name: String,
    age: Number,
    hobbies: [String],
    birthday: Date,
    bestFriend: {
        type: mongoose.SchemaTypes.ObjectId,
        ref: "User"
    },
    favoriteThings: [],
    address: addressSchema
});
```

## Validation de schéma

Afin de validé qu'un champ est requis ou qu'il doit être conforme à certaines règles, un validation du schéma s'impose. Celle-ci est relativement simple, il suffit de transformer une donné en un objet dans notre schéma, de décrire son type et ensuite de décrire la validation que nous voullons y faire à l'aide des différents validateurs.

### Liste de validateurs

Voici la liste des validateurs, leur types applicables (puisque certain validateur ne va pas avec certain type de données) et le type de valeur qu'il faut lui donné : 
| Validateur | Types applicables | Valeur du validateur | Description                                                                        |
|------------|-------------------|----------------------|------------------------------------------------------------------------------------|
| required   | Tous              | Bool                 | Indique que le champ doit être remplit.                                            |
| default    | Tous              | Valeur               | Indique une valeur par défaut.                                                     |
| immutable  | Tous              | Bool                 | Indique que le champ, une fois qu'une valeur y est attribué, ne peut être modifié. |
| lowercase  | String            | Bool                 | Appel la méthode `toLowerCase()` sur le champ.                                     |
| uppercase  | String            | Bool                 | Appel la méthode `toUpperCase()` sur le champ.                                     |
| trim       | String            | Bool                 | Appel la méthode `trim()` sur le champ.                                            |
| match      | String            | Regex                | Vérifie si la string match avec le Regex donné.                                    |
| minLength  | String            | Number               | Vérifie si la string est plus longue que le nombre donné.                          |
| maxLength  | String            | Number               | Vérifie si la string est plus petite que le nombre donné.                          |
| enum       | String, Number    | Tableau, Number      | Vérifie si la valeur du champ est dans le tableau donné.                           |
| min        | Number, Date      | Number, Date         | Vérifie si la valeur du champ est plus grande que la valeur donné.                 |
| max        | Number, Date      | Number, Date         | Vérifie si la valeur du champ est plus petite que la valeur donné.                 |

### Exemple

Voici un exemple de validation : 

```javascript
const mongoose = require('mongoose');

const addressSchema = new mongoose.Schema({
    zipCode: String,
    number: Number,
    street: String,
    city: String
});

const userSchema = new mongoose.Schema({
    name: {
        type: String,
        default: 'Unnamed',
        unique: true
    },
    age: {
        type: Number,
        min: 0,
        max: 125
    },
    hobbies: [String],
    birthday: {
        type: Date,
        immutable: true
    },
    bestFriend: mongoose.SchemaTypes.ObjectId,
    favoriteThings: [],
    address: {
        type: addressSchema,
        required: true
    }
});

module.exports = mongoose.model('User', userSchema);
```

**Note** : Veuillez noter que `unique` n'est pas un validateur, celui-ci créer un indexe unique pour ce champ (je suis pas sur d'avoir compris mais c'est pas un validateur plus d'information [ici](https://masteringjs.io/tutorials/mongoose/unique). <br>
**Note 2** : Il est aussi possible de mettre une fonction à un validateur comme `default` par exemple.

```javascript
function returnShibougameau() {
    return "Shibougameau";
}

const addressSchema = new mongoose.Schema({
    zipCode: String,
    number: Number,
    street: String,
    city: {
        type: String
        default: () => returnShibougameau();
    }
});
```

### Validation personnalisé 

Parfois il pourrait être utile de faire ses propres validateurs et mongoose permet de faire ça! Simplement en ajoutant un validateur nommé `validate` à votre schéma. Ce validateur à la syntaxe d'un objet et fonctionne un peu comme un `if` (donc il est basé sur un condition que nous définissons). À l'intérieur du `validate` nous avons le champ `validator` qui est notre condition (fonction) qui retourne `true` ou `false` et `message` qui est le message (mais aussi, encore une fois, une fonction) d'erreur si jamais la condition n'est pas respecté. En voici un exemple :

```javascript
const userSchema = new mongoose.Schema({
    name: String
    age: {
        type: Number
        validate: {
            validator: v => v % 2 === 0,
            message: props => `${props.value} is not an even number`
        }
    }
});
```

**Note** : `props.value` est la valeur du champ,  de `age` dans l'occurrence. <br>
**NOTE SUPER-MÉGA-GIGA-IMPORTANTE** : Toute validation n'est exécuter SEULEMENT que par les fonctions `save()` et `create()` de notre modèle ET NON PAR LES FONCTIONS COMME `findOneAndUpdate()` ou `findByIdAndUpdate()` etc. donc faites attention quand vous utilisez les autres fonctions "built-in" de Mongoose.

## Fonctionalitées de schéma

Dans cette section, nous verrons de multiples façons de rajouter un certain niveau de fonctionnalité à nos schémas au lieu qu'ils ne soient que des moules à document MongoDB.
**Note** : Dans cette section, j'utilise délibérement des fonctions qui ne sont pas des fonctions flèches parce que autrement, nous n'avons pas accès au mot clef `this` ce qui rend les fonctions un peu inutile.

### Méthodes de schéma

Les méthodes de schéma permettent d'indiqué des actions à faire avec les données de vos modèles (donc les instances de vos schémas). Pour ce faire, il suffit d'ajouter une fonction et de passé ladite fonction à `nomDuSchema.methods.nomDeLaFonction`. Par exemple si je veux que chaque utilisateur ait une fonction pour dire bonjour : 

```javascript
userSchema.methods.sayHi = function () {
    console.log(`Hi! my name is ${this.name}`);
}
```

### Statique de schéma

Les statiques de schéma permettent d'indiqué des actions à faire avec le schéma lui même. Pour ce faire, il suffit d'ajouter une fonction et de passé ladite fonction à `nomDuSchema.statics.nomDeLaFonction`. Par exemple avec une statique de schéma on pourrait définir notre propre fonction de recherche :

```javascript
userSchema.methods.findByName() = function (name) {
    return this.find({ name: new RegExp(name, "i")});
}
```

### Fonction-requête de schéma

Les fonctions-requête de schéma permettent d'indiqué des actions à faire avec le schéma lui même comme dans une requête. Cela signifie que vous pouvez utilisé cette fonction dans une enchainement de d'autres fonction-requêtes prédéfini comme `where()`. Pour ce faire, il suffit d'ajouter une fonction et de passé ladite fonction à `nomDuSchema.query.nomDeLaFonction`. Par exemple :

```javascript
userSchema.query.byName() = function (name) {
    return this.where({ name: new RegExp(name, "i")});
}
```

**Note** : Cette fonction `byName()` sera maintenant disponible parmit les [fonction-requêtes de mongoose](./Bases.md#fonctions-de-requête-mongoose) et pourra être utilisé comme telle.

### Virtuels de schéma

Les virtuels de schéma permettre de "construire" d'autres données (un peu comme rajouter un champ) à partir de ce qui se trouve déja dans le modèle sans avoir à conserver lesdites données dans le document (puisque ça ferait de l'information en double). Par exemple, dans un schéma ou j'ai déjà le nom et l'email d'un utilisateur et que je veux ces deux informations sous forme d'une seule et unique propriété, le virtuel devient utile et rempli exactement cette tache. <br><br>
Pour ce faire, il suffit d'ajouter une fonction à `nomDuSchema.virtual("nomDeLaPropriete").get()` en la passant en tant que paramêtre dans le `get()`. Exemple :

```javascript
userSchema.virtual("nomEmail").get(function () {
    return `${this.name} \t\t <${this.email}>`;
})
```

Et maintenant, la propriété nomEmail est disponible sur un modèle, tout comme la propriété "name" et le tout sans avoir à modifier le schéma ou à duppliquer l'information dans le document.

## Middleware de schéma

Le "middleware" de schéma est une façon d'insérer du code entre (plus précisément avant et/ou après) certaines actions. Pour ce faire, vous devez passer la fonction avec laquelle vous voulez faire dequoi avant ou après à la fonction `pre()` (pour faire du "middleware" avant) ou `post()` (pour faire du "middleware" après) en tant que premier paramètre et en second paramètre, vous passez votre fonction qui est le "middleware". Voici un exemple :

```javascript
userScheme.pre('save', function(next) {
    this.lastUpdated = Date.now();
    next();
});
```

Donc ici, avant tout les appels de la méthode `save()`, nous mettons à jour la propriété "lastUpdated" à la date de maintenant.

**Note** : le `next` est obligatoire dans les paramètres de votre fonction et il sert à dire à mongoose de continuer, de faire ce qu'il doit faire (avec ça on peut enchainé les "middlewares" si on veux).

# Modèle

Les modèles sont les objets résultant de l'utilisation de nos schéma, par exemple, la variable `user` dans l'exemple précédant est notre modèle.

## Création d'un modèle

### Multi-étape

Pour sauvegarder les modèles dans votre BD Mongo, il suffit d'appeler la méthode `save()` de votre modèle précédemment créer. Il est aussi possible, vue que `save()` est une fonction async, d'exécuter une fonction `then()` par dessus la fonction `save()` pour ensuite lui passer une fonction pour décrire ce que l'on veux qu'elle fasse une fois que le modèle est sauvegardé dans la BD. En voici un exemple : 

```javascript
const mongoose = require('mongoose');

const User = require('./User'); //Importation

mongoose.connect('mongodb://localhost/testdb');

const user = new User({name: 'Bob', age: 2}); //Création

//Sauvegarde
user.save().then(() => {
    console.log(`user : ${user.name} saved\n`)
}); 
```

Si vous préférez la syntaxe avec async await, vous pouvez l'utilisé : 

```javascript
const mongoose = require('mongoose');
const User = require('./User'); //Importation

mongoose.connect('mongodb://localhost/testdb');

makeOneUserAndSave()

async function makeOneUserAndSave() {
    const user = new User({name: 'Bob', age: 2});    //Création
    await user.save();                              //Sauvegarde
    console.log(`user ${user.name} saved\n`);
} 
```

**Note** : La magie la dedans (parce que oui il y à de la magie une peu partout) est que, tout comme mongosh, tant que rien n'est sauvegarder dans une BD, la BD n'existe pas. Ce principe s'applique aussi ici, sauf qu'il s'applique sur le collections ET sur les BD. Donc mongoose s'occupe de créer une collection pour vous pour chaque schéma ET EN PLUS il la renomme pour qu'elle soit au pluriel (pour les noms en anglais dans tout les cas). N'est-ce pas merveilleux? <br>
**Note 2** : Vous allez remarquer que dans votre BD, il va y avoir une donnée que vous n'avez pas spécifier mais qui est là pour chaque document. Le `__v`, tout ce que vous devez savoir c'est que c'est mongoose qui à ajouter cette donnée. <br>
**Note 3** : Il serait plus poli de mettre tout ce qui est création, altération et suppression de données dans un try catch si jamais il y à une erreure.

### Singulière

Si vous souhaitez créer un instance de votre modèle et la sauvegarder en une seule étape, une alternative s'offre à vous et elle fait la même chose que le code dans la métode précédente. Pour ce faire, nous allons utilisé la méthode `create()` de mongoose ainsi : 

```javascript
const mongoose = require('mongoose');
const User = require('./User'); //Importation

mongoose.connect('mongodb://localhost/testdb');

makeOneUserAndSave()

async function makeOneUserAndSave() {
    const user = await User.create({name: 'Bob', age: 2});
    console.log(`user ${user.name} saved\n`);
} 
```

## Mise à jour d'un modèle

Afin de mettre à jour un modèle, il suffit d'apporter les modifications nécéssaire à votre modèle en local et ainsi de re-appeler la méthode `save()` de votre modèle ainsi :

```javascript
const mongoose = require('mongoose');
const User = require('./User'); //Importation

mongoose.connect('mongodb://localhost/testdb');

makeOneUserAndSave()

async function makeOneUserAndSave() {
    const user = await User.create({name: 'Bob', age: 2});
    user.name = 'yeet'; //Modification
    await user.save();  //Re-sauvegarde
    console.log(`user ${user.name} saved\n`);
} 
```

**Note** : Si nécéssaire, faite une requête pour trouver l'utilisateur en question et ensuite, quand vous l'avez en local, vous le modifier et appeler `save()`.

# Requêtes

## Style mongosh

Afin d'effectuer une requête, il suffit d'appeler les même méthodes que dans mongosh, par exemple la méthode `find()`, `findOne()` ou encore `exists()` sur votre modèle et la syntaxe est identique à celle dans mongosh. Cela va de soi pour toute les méthodes offertes par mongoose. Voici un exemple: 

```javascript
async function doStuff() {
    try {
        const user = await User.find({name : "Bob"});
    } catch(e) {
        console.log(e.message);
    }
}
```

**Note** : Malgré que cela peut sembler évident, la méthode `find()` retourne un tableau de modèle et la méthode `findOne()` n'en retourne qu'un.

## Style mongoose

Si vous le souhaitez, mongoose offre des fonctions pour faire des requêtes qui est très plus lisible, fait essentiellement la même chose mais qui ajoute beaucoup de code (donc le résultat est pas très très beau souvent). Voici un exemple : 

```javascript
async function doStuff() {
    try {
        const user = await User.where("name").equals("Bob");
    } catch(e) {
        console.log(e.message);
    }
}
```

**Note** Le principe est que on peux enchainé certaines fonctions pour qu'elles aillent un certain effet, par exemple ceci : 

```javascript
async function doStuff() {
    try {
        const user = await User.where("age").lt(30).gt(18);
    } catch(e) {
        console.log(e.message);
    }
}
```

Dans cet exemple, la fonction `lt()` et `gt()` on tout deux un effet sur le champ `age` et si on met un autre `where()` au bout de cette ligne, les fonctions appelées par la suite auront un impacte sur ce second `where()` et ainsi de suite.

### Fonctions de requête mongoose

| Fonction     | Type du paramêtre | Définition                                                                                                   |
|--------------|-------------------|--------------------------------------------------------------------------------------------------------------|
| `where()`    | String            | On y passe le nom du champ sur lequel on veux faire une recherche.                                           |
| `equals()`   | All               | Vérifie si le champ du dernier `where()` est égal à la valeur du paramètre passé.                            |
| `gt()`       | Number            | Vérifie si le champ du dernier `where()` est plus grand que la valeur du paramètre passé.                    |
| `lt()`       | Number            | Vérifie si le champ du dernier `where()` est plus petit que la valeur du paramètre passé.                    |
| `limit()`    | Number            | Limite le nombre de résultat de la recherche à la valeur du paramètre passé.                                 |
| `select()`   | String            | Limite la recherche au champ passé en paramètre.                                                             |
| `populate()` | String            | Ajoute le document dont l'Id fait partie d'un des champs spécifié du modèle sur lequel on exécute la méthode |

**Note** : La fonction `populate()` va aller sur notre document (dans la BD) et copier-coller les informations (le document au complet) dans le champs spécifier qui avait (avant d'appeler `populate()`) un Id d'un autre document. Cela ne fonctionnera que si le champ spécifie à quel collection il fait référence comme indiqué à la fin de [cette section](./Bases.md#architecture-de-schéma).