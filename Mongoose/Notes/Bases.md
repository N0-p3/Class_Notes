# Bases
## Connexion
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
## Schéma
### Définition
Un schéma est une définition d'une collection. En gros, vue que MongoDB permet de mettre des documents ayant une structure différente dans une même collection, mongoose "patch" ça avec ce qu'on appel des schémas. Ces schéma ne vont non seulement définir la structure de nos collections mais aussi, par le fait même définir la structure de nos objets (documents ou modèles) qui seront envoyés à notre base de donné.
### Création d'un schéma
Afin de créer un schéma, nous devons faire un fichier javascript qui va contenir notre schéma et s'assurer que mongoose y est importé, ensuite il suffira de mettre ce schéma dans une variable et de définir notre schéma avec des paires clef-type (comme les documents dans MongoDB) séparer par une virgule. Ensuite, il faudra créer un modèle de ce schéma. Pour ce faire, nous allons utilisé la méthode `model()` de mongoose en lui passant le nom du schéma ainsi que le schéma que nous avons stocker dans une variable précédement. Pour terminer il ne restera plus qu'à exporter le modèle. Le code ressemblera essentiellement à ceci : 
```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    name: String,
    age: Number
});

module.exports = mongoose.model('User', userSchema);
```
**Note** : Les types de mongoose sont disponibles [ici](https://mongoosejs.com/docs/schematypes.html).<br>
### Utilisation d'un schéma
Afin d'utiliser un schéma, il suffit de l'importer et de s'en servir pour créer des objets : 
```javascript
const mongoose = require('mongoose');
const User = require('./User'); //Importation

mongoose.connect('mongodb://localhost/testdb');

const user = new User({name: 'Bob', age: 2}); //Utilisation
```
## Modèle
Les modèles sont les objets résultant de l'utilisation de nos schéma, par exemple, la variable `user` dans l'exemple précédant est notre modèle.
### Sauvegarde d'un modèle
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
**Note** : La magie la dedans (parce que oui il y à de la magie une peu partout) est que, tout comme mongosh, tant que rien n'est sauvegarder dans une BD, la BD n'existe pas. Ce principe s'applique aussi ici, sauf qu'il s'applique sur le collections ET sur les BD. Donc mongoose s'occupe de créer une collection pour vous pour chaque schéma ET EN PLUS il la renomme pour qu'elle soit au pluriel (pour les noms en anglais dans tout les cas). N'est-ce pas merveilleux?