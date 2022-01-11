# Modules
## Théorie
Chaque fichier .js rouler dans node.js est "wrapper" dans une fonction et c'est ce "scope" qu'on confond souvent avec le "scope" globale. Le hic, c'est que le "scope" dans lequel on se trouve lorsque l'on écrit du code dans un fichier .js (rouler dans node.js) est enfait le scope de cette fonction et cette fonction se trouve elle même dans un module. Donc les modules sont comme cette grosse pièce dans le moteur de node.js qui représente un fichier. 
<br><br>
Cette fonction qui enveloppe notre code se nomme la "Module wrapper function" et à certains paramètres que nous pouvons utiliser (mais pas redéfinir). Veulliez inspecté la table suivante pour plus d'information :
| Noms       | Définitions                  |
|------------|------------------------------|
| exports    | Les modules exportés.        |
| require    | ???                          |
| module     | Le module.                   |
| __filename | Le nom du fichier du module. |
| __dirname  | Le nom du dossier du module. |

## Création d'un module (sous forme d'objet)
Dans le fichier ou vous voulez créer du code a exporter vers un autre fichier, faite les étapes suivantes : 
1. Créer un autre fichier .js avec du code (par exemple une fonction).
2. Ajouter dans ce même fichier la ligne suivante (Note : ceci fonctionne aussi avec des variables) : 

```javascript
module.exports.nomDeLaChoseUneFoisExporter = nomDeLaChoseAExporter;
```
## Chargement d'un module (sous forme d'objet)
Dans le fichier ou vous voulez importer du code, faite les étapes suivantes : 
Note : 
1. Utiliser la fonction require() pour importer ce que le fichier spécifie qu'il à a exporter de cette façon : 

```javascript
const foo = require('../Path/Vers/Le/Fichier/A/Importer.js');
```
2. Utiliser votre fichier importé à l'aide de la variable créer à l'étape précédante ainsi : 
```javascript
foo.nomDeLaChoseUneFoisExporter             //Variable
foo.nomDeLaChoseUneFoisExporter(a, b, c)    //Fonction
```
## Création d'un module (sous forme singulière)
Dans le fichier ou vous voulez créer du code a exporter vers un autre fichier, faite les étapes suivantes : 
1. Créer un autre fichier .js avec du code (par exemple une fonction).
2. Ajouter dans ce même fichier la ligne suivante (Note : ceci fonctionne aussi avec des variables) : 

```javascript
module.exports = nomDeLaChoseAExporter;
```
## Chargement d'un module (sous forme singulière)
Dans le fichier ou vous voulez importer du code, faite les étapes suivantes : 
Note : 
1. Utiliser la fonction require() pour importer ce que le fichier spécifie qu'il à a exporter de cette façon (sauf que ici, foo est la chose singulière que nous avons préciser d'exporter lors de la création précédante et non un objet qui contient la fonction ou la variable) : 

```javascript
const foo = require('../Path/Vers/Le/Fichier/A/Importer.js');
```
2. Utiliser votre fonction ou variable importée ainsi : 

```javascript
foo             //Variable
foo(a, b, c)    //Fonction
```
## Module Path
Voici la [Documentation officielle](https://nodejs.org/dist/latest-v17.x/docs/api/path.html) si vous en avez besoin.
<br><br>
Ce module sert à travaillier avec des paths de fichiers et de dossiers. Pour commencer il suffit de l'inclure ainsi :

```javascript
const path = require('path');
```
Le module "Path" peux faire un objet path avec un chemin vers un fichier à l'aide de la fonction parse, ainsi :

```javascript
let pathObj = path.parse(__filename);
``` 
L'objet donnée par cette fonction ressemble à ceci :
| Propriétés | Donnée                                            |
|------------|---------------------------------------------------|
| root       | '/'                                               |
| dir        | '/home/void/Documents/Programming/Js/Node.js/Exp' |
| base       | 'test.js'                                         |
| ext        | '.js'                                             |
| name       | 'test'                                            |

**Note** : Il est donc plus facile d'utiliser le module Path si il nous faut gosser avec un path que si nous utilisions une string.
## Module OS
Voici la [Documentation officielle](https://nodejs.org/dist/latest-v17.x/docs/api/os.html) si vous en avez besoin.
<br><br>
Ce module sert à obtenir de l'information sur l'OS ou passer par l'OS pour aller chercher de l'informations à propos de la machine, pour commencer il suffit de l'inclure ainsi :

```javascript
const os = require('os');
```
Exemple d'usage du module OS : Aller chercher la quantité de mémoire totale et la quantité de mémoire libre : 
```javascript
let totalMem = os.totalmem();
let freeMem = os.freemem();

console.log(`Mémoire totale : ${totalMem} \nMémoire libre : ${freeMem}`);
```
Affichage à la console :
```
Mémoire totale : 12347944960 
Mémoire libre : 6432976896
```
## Module File System
Voici la [Documentation officielle](https://nodejs.org/dist/latest-v17.x/docs/api/fs.html) si vous en avez besoin.
<br><br>
Ce module permet d'intéragir avec les fichiers (écrire, lire créer et supprimer), pour commencer il suffit de l'inclure ainsi :

```javascript
const fs = require('fs');
```
**Note** : La plupart des fonctions dans le module File System sont en double, une version est la version synchrone et l'autre est asynchrone. Par exemple `access()` est async et `accessSync()` est synchrone. De plus, toutes fonctions asynchrones prennent un argument de plus, l'argument se trouve à être une fonction qui est appelé une fois que l'opération est terminé (c'est la callback function).
<br><br>
Exemple d'usage du module File System :

```javascript
//Manière synchrone
const files = fs.readdirSync('./');
console.log(files);

//Manière asynchrone
fs.readdir('./', (err, files) => {
    if (err) {console.log(err);}
    else {console.log(files);}
});
```
## Module Event
Voici la [Documentation officielle](https://nodejs.org/dist/latest-v17.x/docs/api/events.html) si vous en avez besoin.
<br><br>
Ce module permet de créer des évènements et de les gérer (faire l'abonement d'une fonction à une autre, de les décrires et etc.). Pour commencer il suffit de l'inclure ainsi :

```javascript
const EventEmitter = require('events');
//instanciation
const emitter = new EventEmitter();
```
**Note** : Remarquez que j'ai délibérement écrit `EventEmitter` en UpperCamelCase, j'ai fait cela puisque le retour de ce require n'est pas un module mais bien une classe (et non un objet). Ce qui explique la seconde ligne ou je fait une instance (un objet) de cette classe que j'ai importé.
<br><br>
Voici un exemple très simple d'un événement élevé (Raise an event) et d'un abonnement à cet évènement (Register a listener) :

```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

//Register to an event
emitter.on('eventName', () => {
    console.log('Fait quelque chose...');
});

//Raise an event
emitter.emit('eventName');
```
**Explication** : Donc en gros, nous avons fait un "listener" qui écoute si un évènement au nom de `eventName` est levé et on lui passe une fonction qui est la fonction qui sera exécuter lorsque l'évènement sera levé (dans mon cas j'ai fais une fonction flèche anonyme qui ne fait que "logger" quelque chose).
<br><br>
Et ensuite nous avons levé l'évènement avec la fonction `emit()` en lui passant le nom de l'évènement à levé!
<br><br>
En bref :
la fonction `on()` **OU** `addListener()` ajoute un listener à un évènement et la fonction `emit()` appel l'évènement passé en paramètre.

### Argument d'évènement
Parfois, il serait utile de non seulement levé un évènement mais aussi d'envoyer des données lorsque l'on lêve un évènement à la fonction qui écoute sur cet évènement en question. Pour ce faire il suffit de passé dans la fonction `emit()` un objet contenant