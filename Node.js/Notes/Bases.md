# Bases
## Données et déclaration
### Variables
`let` est utilisé pour créer des variables de tout types et `const` est utilisé pour créer des constantes de tout types, les deux s'utilisent de la façon suivante : 

```javascript
let a = 1;
let b = true;
let c = 'tamere';
const d = 2;
const e = false;
const f = 'tonpere';
```
Les déclarations peuvent aussi être séparés par des virgules pour être sur une même ligne (si `let` est placer au début, toutes les variables seront variables et inversement pour `const`) :

```javascript
let g = 'Geofroy', h = true, i = 480;
```
### Tableaux
On utilise tout le temps `const` puisque un tableau est en théorie immuable, celui-ci se déclare ainsi (la déclaration peut se faire sur une ou plusieurs lignes) :

```javascript
const voitures = ["Saab", "Volvo", "BMW"];                                   //Avec données
const jeux = [];                                                             //Sans données
const pays = new Array("Canada", "État-Unis", "France", "Espagne", "Maroc"); //Avec le mot clef new

//Ajout de données (même si jeux est un const)
jeux[0] = 'Skyrim';
jeux[1] = 'The Witcher III : The Wild Hunt';
jeux[2] = 'tamere : la pute';
```
**Note** : La déclaration d'un tableau avec le mot `new` peut causer des comportements inattendus, exemple : 

```javascript
//Créer un tableau avec 1 élément 
const chiffres1 = [40];
//Créer un tableau avec 40 éléments
const chiffres2 = new Array(40);
```
**Note 2** : Membre important d'un tableau : 

| Membre    | Description                                        |
|-----------|----------------------------------------------------|
| push()    | Ajouter un élément au tableau.                     |
| forEach() | Itérer sur le tableau (en y passant une fonction). |
| join()    | Fait une grosse string avec le contenu du tableau. |
| length    | Retourne la longueur du tableau.                   |

**Note 3** : On peut mettre tout type de données **CONFONDUES** dans un tableau incluant des objets et des fonctions (apparement).
#### Syntaxe étendue (spread syntax)
La syntaxe étendue permet de dire "prend tout les données dans ce tableau", exemple :

```javascript
let a = ['un', 'deux'];
let b = ['trois', 'quatre'];

let c = [...a, ...b];
console.log(c); //Résultat : [ 'un', 'deux', 'trois', 'quatre' ]
```
Avec cette syntaxe nous pouvons donc faire des `push` ou des `unshift` manuellement de plusieur choses en même temps (et de manière plus belle) :

```javascript
let a = ['un', 'deux', 'trois', 'quatre'];

//Push
a = [...a, 'cinq', 'six', 'sept'];

//Unshift
a = ['moins un', 'zero', a...];
```
### Objet
Un objet sert a réunir des données ensemble pour faciliter la représentation de quelque chose (abstrait ou pas). Normalement, on doit avoir une classe pour faire des objets mais pas en Javascript parce que ... Javascript. On utilise tout le temps `const` puisque c'est une norme, celui-ci se déclare ainsi (la déclaration peut se faire sur une ou plusieurs lignes) :

```javascript
const voiture = {type:'Fiat', model:'500', color:'white'};
```
On peut aussi accéder au donnée d'un objet de plusieurs manières :

```javascript
voiture.type
voiture['type']
```
**Note** : On peut stocker des fonctions (que l'on va par la suite appelé méthodes) dans un objet et les appelés ainsi :

```javascript
const voiture = {   type:'Fiat', 
                    model:'500', 
                    color:'white',
                    setColor : function(newColor) {
                        this.color = newColor;
                    }
                };
voiture.setColor('green');
```
**Note 2** : NE PAS CRÉER DE VARIABLES DE TYPE PRIMAL EN TANT QU'OBJET, C'EST MAL! (ralenti l'éxécution et complique le code).
Exemple **A NE PAS FAIRE** :

```javascript
x = new String();
y = new Number();
z = new Boolean(); 
```
### Classe
Les classes sont les moules à objets OO de Javascript. Le "boilerplate code" d'une classe en Javascript est le suivant :
```javascript
class ClassName {
    constructor(parameter1, parameter2) {
        this.property1 = parameter1;
        this.property2 = parameter2;
    }
    doStuff() {
        //code
    }
}
```
Afin de déclarer un objet à partir d'une classe, il suffit d'écrire le code suivant :
```javascript
let foo = new ClassName(parameter1, parameter2);
```
#### Déstructurisation
Si nous avons une fonction qui prend en paramètre un objet mais que nous n'utilisons que quelques unes de ces propriétés, la déstructurisation est optimale. La déstructurisation permet de minimiser la répétition de code en plaçant les propriété nécessaire d'une fonction dans un objet reçu en paramètre d'une fonction. En voici un exemple :
<br>
<br>
Imaginons que nous avons un objet représentant une tortue et que nous voulons y faire une fonction qui nourrit l'animal (elle ne fera qu'imprimer de l'information à la console).

```javascript
const turtle = {
    name: 'Bob',
    health: 10,
    biteForce: 15,
    legs: 4,
    shell: true,
    type: 'amphibious',
    meal: 10,
    diet: 'berries'
}
//Fonction normale (mauvaise)
function feed(animal) {
    console.log(`Fed ${animal.name} ${animal.meal} ${animal.diet}`);
}
//Fonction déstructurisé (bonne)
function feedDestructured({name, meal, diet}) {
    console.log(`Fed ${name} ${meal} ${diet}`);
}
```
**Note** : Le code n'est pas nécéssairement plus court dans cet exemple-ci mais dans un exemple avec un plus gros objet ou nous devions utiliser à mainte reprise plusieurs des propriétés, la déstructurisation devient optimale.

## Blocs conditionnels
### If
La syntaxe du `if` va comme suit :

```javascript
if (condition1) {
    //code
} else if (condition2) {
    //code
} else {
    //code
}
```
### Inline if
La syntaxe du inline if va comme suit :
```javascript
let c = ((a < b) ? true : false);
```
Si la condition est vraie, `true` sera associer à `c` sinon `false` y sera associé. <br>**Note** : Le inline if est entourer de parenthèses.
### Switch
La syntaxe du `switch` va comme suit :

```javascript
switch(expression) {
    case x:
        //code
        break;
    case y:
        //code
        break;
    default:
        //code
} 
```

## Boucles
### For
La syntaxe du `for` va comme suit :

```javascript
for (let i = 0; i < 10; i++) {
    //code
}
```
### While
La syntaxe du `while` va comme suit :

```javascript
while (condition) {
    //code
}
```
### Do While
La syntaxe du `do while` va comme suit :

```javascript
do {
    //code
}
while (condition);
```
## Fonctions
La syntaxe d'une fonction va comme suit :

```javascript
function myFunction(p1, p2) {
    //code
}
```
**Note** : La fonction peut retourner quelque chose ou pas et prendre des paramètres ou pas.
### Appel de fonctions
L'appel d'une fonction est très simple, il suffit d'écrire son nom et de lui donner ses paramètres entre parenthèses et si celle-ci appartient à un objet, l'appeler à partir de son objet ainsi : 

```javascript
sum(2, 2);          //fonction globale
person.getAge();    //fonction d'un objet
```
## Fonctions anonymes
Les fonction anonymes sont des fonctions qui au lieu d'être instanciée dans une variable ne sont jamais instanciée et plutôt définies sur le champs, en voici un exemple :

```javascript
setTimeout(function() {
    console.log('Execute later after 1 second');
}, 1000);
```
**Explication** : La fonction `setTimeout()` nécéssite une autre fonction en paramètre, sauf que au lieu de définir cette fonction au paravent et de la passer ensuite en paramètre, on la définit sur le champs et ensuite on continue à passer les paramètre que `setTimeout()` attend, comme si de rien.
## Fonctions flèches
Les fonctions flèche (arrow function) sont une autre façon d'écrire une fonction qui est particulièrement utile lors de l'écriture de fonctions anonymes. Voyons, à l'aide d'étapes, comment transformer une fonction simple en un fonction flèche encore plus simple.
<br><br>
Voici la fonction de base : 

```javascript
function sum(a, b) {
    return a + b;
}
``` 
la première étape est de se débarasser du mot clef `function` et de mettre cette fonction dans une variable :

```javascript
let sum = (a, b) => {
    return a + b;
}
```
Et voila, le tour est joué en majorité. je dit bien en majorité puisque vue que la fonction ne fait qu'une ligne il est possible de la simplifier encore plus avec cette prochaine étape.
<br><br>
Vue que nous n'avons qu'une seule ligne de code nous pouvons retirer les `{}`, mettre le tout sur une seule ligne et enlever le mot clef `return` pusique celui-ci est assumé par javascript, ce qui nous donne :

```javascript
let sum = (a, b) => a + b;
```
**Note** : Si il n'y à qu'un seul paramètre à la fonction, on pourrait enlever les parenthèses entourant les paramètres. <br>
**Note 2** : L'appel de ces fonctions est identique à celui d'une fonction normal.
**Note 3** : Normalement une fonction d'un objet à le mot de clef `this` associé au 'scope' (environnement) d'ou elle est appelée mais avec une fonction flèche, le 'scope' est celui d'ou la fonction flèche est définie. (Ou dequoi du genre la ya quelque chose de casser avec le scope et les fonctions flèche desfois j'ai pas trop compris)
### Fonctions flèches anonymes
Effectivement, les fonctions flèches sont surtout utile lorsque nous devons faire des fonctions anonymes. Voici l'exemple d'un peu plus haut en fonction flèche anonyme :

```javascript
setTimeout(() => {
    console.log('Execute later after 1 second');
}, 1000);
```
**Note** : Nous pouvons simplifier encore plus la chose, si la fonction `setTimeout()` n'avait q'un seul paramètre, nous aurions pus la mettre sur une seule ligne comme vue précédemment dans [Fonctions flèches](#fonctions-flèches)
## Possibles erreurs à l'installation
Voici une mini-liste des erreures que vous pourriez rencontrez durant l'installation, si le lien est coché c'est que la solution à fonctionnée pour moi :) .
<br>
[x] [dpkg: error processing archive unpack](https://github.com/nodesource/distributions/issues/1157)