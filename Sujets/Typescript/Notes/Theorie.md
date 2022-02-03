# Typescript c'est quoi?

Donc, Typescript en fait c'est un peu comme un DLC sur Javascript, y rajoute des fonctionnalitées, des choses de plus que Javascript n'a pas. C'est ce que l'on appel un "superset" de Javascript. Un peu comme C++ est un superset de C, C++ ajoute les classes et le OOP au langage C et bien Typescript ajoute les types, les interfaces et quelques petite chose à coté comme les génériques, les enums et etc.<br><br>
De plus, Typescript est un "compilateur" et je dit bien "compilateur" avec des guillmets puisque en fait on va passé notre code Typescript à `tsc` (le compilateur Typescript) et lui va le "compiler" en code Javascript, donc en fin de compte le langage sert vraiment juste à corriger notre code Javascript avant son éxécution / distribution pour pas qu'on se plante dans mille erreures connes. Le fait que notre code Typescript, à la fin, devient du code javascript permet aussi de faire TOUT CE QUE L'ON CONNAIT DÉJÀ DANS JAVASCRIPT (en configurant notre compilateur comme il se doit bien sur!). Ceci étant dit, même si Typescript rajoute les types dans Javascript, ceux-ci sont optionnel et non obligatoire! <br><br>
Le "compilateur" est bien sur configurable non seulement sur ce dernier point mais aussi sur de nombreux aspects, nous couvrirons quelques uns de ces points plus tard :). <br><br>

# Installation

## Windows

Pour les utilisateurs de WiNdOwS (ouache), vous pouvez installer Typescript ainsi :

1. Assurez-vous d'avoir npm d'installé (ce qui devrait être fait si vous avez installé Node.js).
2. Exécutez la commande suivante `npm install -g typescript` dans un terminal (PAS POWERSHELL).
3. Confirmer que vous avez bien Typescript avec `tsc -v`.

## Linux

Pour nous, cher utilisateur Linux, afin d'installer le compilateur Typescript, il nous suffit d'installer un seul paquet :

1. Installer le paquet `node-typescript` avec la commande suivante `sudo apt install node-typescript` (utilisez votre fournisseur de paquet dans le cas ou vous n'avez pas apt).
2. Confirmer que vous avez le paquet avec `tsc -v`.

# Configuration du compilateur

Afin de débuter la configuration du compilateur, il nous faut générer le fichier de configuration de ce dernier. Pour ce faire, exécuter la commande suivante :

```
tsc --init
```

Ainsi, dans le dossier actuel vous aurez maintenant le fichier `tsconfig.json`. <br><br>

Par la suite, nous allons changer la version de la compilation (puisque Typescript compile, par défaut, en Javascript ES5 qui est légèrement "out-of-date") et modifier les dossiers "in" et "out". Pour ce faire suivez les étapes suivantes :

1. Ouvrez le fichier `tsconfig.json`.
2. Trouver `"target":` sous `"compilerOptions":` et changer sa valeur pour `"es6"`. 
3. Trouver `"outDir":` sous `"compilerOptions":` et changer sa valeur pour le "path" où vous voulez que vos fichiers compilés se trouvent (post-compilation, donc les fichiers Javascripts).
4. Décommenter la ligne du `"outDir":`.
5. Trouver `"rootDir":` sous `"compilerOptions":` et changer sa valeur pour le "path" où vous voulez que TypeScript prenne les fichiers à compiler (pré-compilation, donc les fichiers Typescript).
6. Décommenter la ligne du `"rootDir":`.

# Utilisation du compilateur

Afin de compiler votre projet, il suffit d'exécuter la commande suivante : `tsc` n'importe où dans votre projet (après avoir générer votre fichier de configuration).