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