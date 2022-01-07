# Modules
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