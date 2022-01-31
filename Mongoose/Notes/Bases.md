<style>
    .title{
        font-size: 37px;
        text-align: center;
        border-bottom: solid rgb(143, 143, 143);
        border-width:2px;
    }
</style>

<p class="title"> Bases </p>

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
Pour ce qui est de travailler avec ce schéma c'est comme avant sauf qu'il y à maintenant plus de données dans votre modèle à créer et chacun d'entre eux doit contenir le bon type.

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