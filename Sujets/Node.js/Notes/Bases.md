# Données et déclaration

## Variables

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

## Tableaux

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

### Syntaxe étendue (spread syntax)

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

## Objet

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

## Classe

Les classes sont les moules à objets OO de Javascript. Le "boilerplate code" d'une classe en Javascript est le suivant :

```javascript
class Person {
    name;
    age;
    sex;

    constructor(name, age, sex) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }

    makeOlder(years) {
        this.age += years;
    }
}
```

Afin de déclarer un objet à partir d'une classe, il suffit d'écrire le code suivant :

```javascript
let tamere = new Person('tamere', 69, true);
```

### Déstructurisation

Si nous avons une fonction qui prend en paramètre un objet mais que nous n'utilisons que quelques unes de ces propriétés, la déstructurisation est optimale. La déstructurisation permet de minimiser la répétition de code en plaçant les propriété nécessaire d'une fonction dans un objet reçu en paramètre d'une fonction. En voici un exemple :
<br><br>
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

### Héritage

Afin de créer une classe qui hérite d'une autre classe, il suffit d'utilisé le mot clef `extends` après la définition de la classe ainsi :

```javascript
class Employee extends Person {
    id;

    constructor(id, name, age, sex) {
        super(name, age, sex);
        this.id = id;
    }
    doStuff() {
        //code
    }
}
```

Ainsi, la classe `Employee` hérite de `Person` ainsi que de tout ses membres. <br><br>

**Note** : Si vous souhaitez appeler le constructeur de la classe parent dans le constructeur d'une classe enfant, il suffit d'utiliser la fonction `super()` comme précisé dans l'exemple précédent. <br>
**Note 2** : Il est important d'appeler le constructeur du parent avant tout sinon Node.js aime pas ça! 

# Blocs conditionnels

## If

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

## Inline if

La syntaxe du inline if va comme suit :

```javascript
let c = ((a < b) ? true : false);
```

Si la condition est vraie, `true` sera associer à `c` sinon `false` y sera associé. <br>**Note** : Le inline if est entourer de parenthèses.

## Switch

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

## Try / catch

Le try / catch sert à la gestion d'erreur dans un bout de code qui pourrait potentiellement planter. Si javascript rencontre une erreure peu importe où (dans le try), peu importe comment, javascript exécutera le code dans le catch. La syntaxe du try / catch va comme suit : 

```javascript
try {
    //code
} catch (error) {
    //code
}
```

# Boucles

## For

La syntaxe du `for` va comme suit :

```javascript
for (let i = 0; i < 10; i++) {
    //code
}
```

## While

La syntaxe du `while` va comme suit :

```javascript
while (condition) {
    //code
}
```

## Do While

La syntaxe du `do while` va comme suit :

```javascript
do {
    //code
}
while (condition);
```

# Fonctions

La syntaxe d'une fonction va comme suit :

```javascript
function myFunction(p1, p2) {
    //code
}
```
**Note** : La fonction peut retourner quelque chose ou pas et prendre des paramètres ou pas.

## Appel de fonctions

L'appel d'une fonction est très simple, il suffit d'écrire son nom et de lui donner ses paramètres entre parenthèses et si celle-ci appartient à un objet, l'appeler à partir de son objet ainsi : 

```javascript
sum(2, 2);          //fonction globale
person.getAge();    //fonction d'un objet
```

# Fonctions anonymes

Les fonction anonymes sont des fonctions qui au lieu d'être instanciée dans une variable ne sont jamais instanciée et plutôt définies sur le champs, en voici un exemple :

```javascript
setTimeout(function() {
    console.log('Execute later after 1 second');
}, 1000);
```

**Explication** : La fonction `setTimeout()` nécéssite une autre fonction en paramètre, sauf que au lieu de définir cette fonction au paravent et de la passer ensuite en paramètre, on la définit sur le champs et ensuite on continue à passer les paramètre que `setTimeout()` attend, comme si de rien.

# Fonctions flèches

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

**Note** : Si il n'y à qu'un seul paramètre à la fonction, on pourrait enlever les parenthèses entourant les paramètres.<br>
**Note 2** : L'appel de ces fonctions est identique à celui d'une fonction normal. <br>
**Note 3** : Normalement une fonction d'un objet à le mot de clef `this` associé au 'scope' (environnement) d'ou elle est appelée mais avec une fonction flèche, le 'scope' est celui d'ou la fonction flèche est définie (ou dequoi du genre la ya quelque chose de casser avec le scope et les fonctions flèche desfois j'ai pas trop compris).

## Fonctions flèches anonymes

Effectivement, les fonctions flèches sont surtout utile lorsque nous devons faire des fonctions anonymes. Voici l'exemple d'un peu plus haut en fonction flèche anonyme :

```javascript
setTimeout(() => {
    console.log('Execute later after 1 second');
}, 1000);
```

**Note** : Nous pouvons simplifier encore plus la chose, si la fonction `setTimeout()` n'avait q'un seul paramètre, nous aurions pus la mettre sur une seule ligne comme vue précédemment dans [Fonctions flèches](#fonctions-flèches)

# Promesses

Les promesses en javascript sont des objets qui, tout comme une promesse dans la vraie vie, promet de faire quelque chose lorsque quelque chose d'autre est terminer. C'est comme si le code disait : "Jte promet dude que j'va exécuter ste fonction là si toute la patente marche. J'te le jure!". La magie la dedans c'est que on peux lui dire de faire quelque chose après une action qui peux prendre beaucoup de temps comme un téléchargement ou une requête à un API. De plus, il est possible de passé du stock (variables, objets, tableau, you name it) d'une promesse à la fonction qu'elle doit exécuter tout dépendament si elle se résolue (succès) ou si elle échoue. Donc, voyons un exemple (avec syntaxe pédagogique) d'une promesse : 

```javascript
let promise = new Promise((resolve, reject) => {
    let foo = 1 + 1;
    if (foo === 2) {
        resolve('Succès!');
    } else {
        reject('Échec!');
    }
});

promise.then((message) => {
    console.log(`Ceci est exécuter dans le then, puisque la promèsse fut résolue. Message : ${message}`);
}).catch((message) => {
    console.log(`Ceci est exécuter dans le catch, puisque la promèsse à échoué. Message : ${message}`);
});
```

**Explication** : Donc en gros ici, on décrit notre promesse en y passant une fonction flèche anonyme (remarqué que la fonction dans la promesse prend deux paramètres, `resolve` et `reject` qui sont les fonctions qu'on va appelés plus tard, vous pouvez les nommer comme bon vous semble) et si le résultat est bon on appel la méthode `resolve()` avec un message et dans le cas contraire on appel la méthode `reject()` avec un autre message! <br><br>
Suite à la description de notre promesse, on décris sont agissement dépendant de quelle fonction notre promesse va appeler (donc si il y à succès ou échec) une fois que son exécution est terminer (dans le `promise.then().catch()`). Dans le `then()` on passe une autre fonction flèche anonyme qui elle reçoit le paramètre du `resolve()` et dans cette fonction on décris ce que l'on veux faire si la promèsse est un succès (et inversement, dans le `catch()` on décris ce que l'on veux faire si la promèsse échoue). <br><br>
**Note** : Il aurait été possible d'écrire le `.then()` immédiatement après la définition de la promesse mais comme préciser précédemment, j'ai préférer utiliser une syntaxe pédagogique par souçis de compréhension.

## Fonctions async / await

Les fonctions "async / await" sont une meilleure façon d'écrire des promesses ou de travailler avec des promesses, la syntaxe fait plus de sens au lecteur et elle est aussi plus plaisante à écrire. Maintenant, nous allons améliorer syntaxiquement la promesse précédante! : 

```javascript
function makePromise() {
    return promise = new Promise((resolve, reject) => {
        let foo = 1 + 1;
        if (foo === 3) {
            resolve('Succès!');
        } else {
            reject('Échec!');
        }
    });
}

async function doStuff() {
    try {
        const message = await makePromise();
        console.log(`Ceci est exécuter dans le then, puisque la promèsse fut résolue. Message : ${message}`);
    } catch (errorMessage) {
        console.log(`Ceci est exécuter dans le catch, puisque la promèsse à échoué. Message : ${errorMessage}`);
    } 
}

doStuff();
```

**Note** : Veuilliez noter que j'ai entouré ma promesse dans une fonction qui la retourne par souçi de beauté, normallement ce n'est même pas nous qui vons faire les promesses mais c'est nous qui allons les recevoir. Tout ça pour dire que ma promesse est entouré par une fonction qui la retourne mais ne vous en faite pas pour ce bout la tant que vous comprenez! <br><br>
**Explication** : On à remplacer notre `.then()` par une fonction qui elle est définit avec le mot `async` ce qui dit à javascript : "Exécute ça sur un autre thread (parce que tu va devoir attendre)". Par la suite, on reçoit le retour de notre promesse que l'on stocke dans une variable `message` en utilisant le mot clef `await`. C'est donc à cette ligne que notre code va attendre et lorsque la promesse est terminée, il va éxécuter la ligne suivante, pas avant! <br><br> Bien sûr si une erreur occure, on tombera alors dans le catch!<br><br>
**Note 2** : Ce type de syntaxe pour les promesses devient particulièrement plus intéressante lorsque nous devons travailler avec des promesses l'une dans l'autre ce qui provoque des `.then()` sur des `.then()` sur des `.then()` et ainsi de suite. <br>
**Note 3** : N'oubliez pas d'appeler votre fonction async sinon rien ne va se passer!