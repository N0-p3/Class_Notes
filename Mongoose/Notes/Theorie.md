# Théorie
## Installation
Afin d'installer Mongoose, assurez vous d'avoir MongoDB, mongosh et Node.js d'installés. Par la suite, assurez-vous de suivre les étapes suivantes
1. Se dirigez dans le dossier de votre projet et ouvrir une console.
2. créer un fichier vide javascript.
3. Initiliser npm avec : `npm init -y`.
4. Installer mongoose avec : `npm i mongoose`.
5. (**OPTIONNELLEMENT**) Installer nodemon avec : `npm i --save-dev nodemon` (nodemon re-exécute votre script chaque fois que vous le sauvegarder pour vous sauvez quelques secondes d'arrêt et de ré-execution).
6. (**OPTIONNELLEMENT**) Indiqué quel script que nodemon doit re-exécuter dans le fichier `package.json` en changeant la ligne dans l'objet `scripts` pour la mienne : 
```
{
  "name": "exp",
  "version": "1.0.0",
  "description": "",
  "main": "test.js",
  "scripts": {
    "project": "nodemon test.js" //ligne que j'ai remplacé
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "mongoose": "^6.1.6"
  },
  "devDependencies": {
    "nodemon": "^2.0.15"
  }
}
``` 
7. (**OPTIONNELLEMENT**) Changer `test.js` pour le nom de votre fichier javascript
**Note** : Pour rouler votre code à l'avenir, utilisé la commande `npm run project` (ce qui va exécuter la commande que vous venez de mettre dans votre fichier `package.json`). Comme vous vous en doutez, oui vous pouvez changer "project" pour ce que vous voulez.