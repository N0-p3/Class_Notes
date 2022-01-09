# Affichage à la console
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
## Afficher le temps dans la console
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