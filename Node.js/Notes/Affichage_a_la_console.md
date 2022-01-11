# Affichage à la console
## Litéraux de modèle (template literals)
Le "template literal" est une façon de contourner la concaténation de chaine tout en affichant les valeurs de certaines variables. Afin de se faire il suffit de s'assurer que la variable est atteignable (donc qu'elle est dans le bon 'scope') et de l'entourer d'un signe de dollar et d'acollades ainsi :

```javascript
function printSum(a, b) {
    let sum = a + b;
    console.log(`The sum of ${a} and ${b} is ${sum}!`);
}
```
**Note** : Faites attention! si vous voulez utiliser cette façon d'afficher des variables à la console, votre string doit être entourée de ` (accents graves) et non de ' (apostrophe) ;) .
## Afficher le nom des variables
**Note** : Prenez compte que le code suivant est compris dans les deux exemples: 

```javascript
const foo = {name: 'Martin', age: 35, competent: true};
const bar = {name: 'David', age: 22, competent: true};
const biz = {name: 'George', age: 36, competent: false};
```
Afin d'associer des noms aux variables quand on les log à la console, il suffit de placer le ou les variables dans un objet, le tout dans un seul console.log (au lieu de faire un console.log par variable). Ainsi, le code ressemble à ceci :

```javascript
console.log({foo, bar, biz});
```
Avec un affichage ressemblant à cela :

```javascript
{
    foo: { name: 'Martin', age: 35, competent: true },
    bar: { name: 'David', age: 22, competent: true },
    biz: { name: 'George', age: 36, competent: false }
}
```
## Afficher les données sous forme de table
Lorsque les données partages tous une même forme (donc qu'ils font parti du même objet) ou qu'ils signifient tous la même chose. Il serait utile de les afficher dans une table. <br><br>
Pour ce faire il suffit de placer les objets (ou les variables) dans un tableau et de les afficher avec `console.table()`. Le code devrait ressembler à ceci :

```javascript
console.table([foo, bar, biz]);
```
Et l'affichage devrait ressembler à ceci :

```javascript
┌─────────┬──────────┬─────┬───────────┐
│ (index) │   name   │ age │ competent │
├─────────┼──────────┼─────┼───────────┤
│    0    │ 'Martin' │ 35  │   true    │
│    1    │ 'David'  │ 22  │   true    │
│    2    │ 'George' │ 36  │   false   │
└─────────┴──────────┴─────┴───────────┘
```
## Afficher le temps à la console
Lorsque nous faisons un benchmark (par exemple) il serait plutôt utile de logger le temps de temps à autre. Ceci peut se faire à l'aide du code suivant :

```javascript
console.time('execution time');
//code
console.timeEnd('execution time')
```
lorsque le code executera `console.timeEnd()` le résultat sera afficher à la console ainsi : 
```
execution time: 77.756ms
```
## Afficher un trace d'exécution
Afin d'afficher ou une fonction fut définie et ou elle fut appelé, il suffit d'appeler la fonction trace de la console et de lui passer un identifiant pour en faire la trace :

```javascript
console.trace('identifiant');
```