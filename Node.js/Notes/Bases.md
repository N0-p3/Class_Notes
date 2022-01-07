# Bases
## Données et déclaration
### Variables
`let` est utilisé pour créer des variables de tout types et `const` est utilisé pour créer des constantes de tout types, les deux s'utilisent de la façon suivante : 
```javascript
let a = 1;
let b = true;
let c = 'tamere'
const d = 2;
const e = false;
const f = 'tonpere'
```
Les déclarations peuvent aussi être séparés par des virgules pour être sur une même ligne (si `let` est placer au début, toutes les variables seront variables et inversement pour `const`) :
```javascript
let g = 'Geofroy', h = true, i = 480;
```
### Tableaux
On utilise tout le temps `const` puisque un tableau est en théorie immuable, celui-ci se déclare ainsi (la déclaration peut se faire sur une ou plusieurs lignes) :
```javascript
const voitures = ["Saab", "Volvo", "BMW"]; //Avec données
const jeux = []; //Sans données
const pays = new Array("Canada", "État-Unis", "France", "Espagne", "Maroc") //Avec le mot clef new

//Ajout de données (même si jeux est un const)
jeux[0] = 'Skyrim';
jeux[1] = 'The Witcher III : The Wild Hunt'
jeux[2] = 'tamere : la pute'
```
**Note** : La déclaration d'un tableau avec le mot `new` peut causer des comportements inattendus, exemple : 
```javascript
//Créer un tableau avec 1 élément 
const chiffres1 = [40];
//Créer un tableau avec 40 éléments
const chiffres2 = new Array(40);
```
**Note 2** : Membre important d'un tableau : 
```javascript
nomDuTableau.push();    //Ajouter au tableau
nomDuTableau.length;    //Longueur du tableau
nomDuTableau.forEach(); //itérer sur le tableau (en y passant une fonction)
nomDuTableau.join()     //Fait une grosse string avec le contenu du tableau
```
**Note 3** : On peut mettre tout type de données **CONFONDUES** dans un tableau incluant des objets et des fonctions (apparement).
### Objet
On utilise tout le temps `const` puisque c'est une norme, celui-ci se déclare ainsi (la déclaration peut se faire sur une ou plusieurs lignes) :
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
const voiture = {type:'Fiat', 
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
**Note** : La fonction peut retourner quelque chose ou pas et prendre des paramêtres ou pas.