# Bases

## Pour commencer

Comme dans plusieurs autres languages, le point d'entrée d'une application en Dart sera la fonction `main()`. Il ne peut y en avoir qu'une seule par application.

```dart
void main() {
    print('Hello, World!');
}
```

## Données et déclaration

### Variables

`var` est utilisé pour créer des variables de tous types et `const` ou `final` sont utilisés pour créer des constantes de tous types, les deux s'utilisent de la façon suivante :

```dart
var a = 1;
var b = true;
var c = 'tamere';
var t = [1,3,5,7];
const d = 2;
const e = false;
final f = 'tonpere';
```

Les variables sont bel et bien typées seulement, le type est inféré à la déclaration. Contrairement à Javascript, on ne peut donc pas assigné à une variable une valeur d'un type différent de celui à sa déclartion

```dart
var a = 1;
a = 'tonpere' // Erreur: A value of type 'int' can't be assigned to a variable of type 'String'.
```

Il est aussi possible de typer manuellement nos variables. `var` devient alors implicite.

**Note:** Les variables peuvent êtres nullable grâce au maginifique `?`

```dart
int a = 1;
bool b = true;
String c = 'tamere';
String? n = null;
const double d = 2.0;
const bool e = false;
final String f = 'tonpere';
```

Vous pouvez déclarer plusieurs variables sur une ligne, mais elles doivent tous être du même type ou passer par `var`, car toute la ligne utilisera le premier type.

```dart
var a = 1, b = 'juif', c = {}, d = [];     // Correct
int a = 1, b = 2, c = 3, d = 4;            // Correct
int a = 1, String b = 'juif', List c = []; // Erreur
```

## Liste des types built-in

### Types basiques

| Type       | Description                                 |
| ---------- | ------------------------------------------- |
| `Numbers`  | int, double                                 |
| `Strings`  | String                                      |
| `Booleans` | bool                                        |
| `Lists`    | List, also known as arrays                  |
| `Sets`     | Set                                         |
| `Maps`     | Map                                         |
| `Runes`    | Runes; often replaced by the characters API |
| `Symbols`  | Symbol                                      |
| `Null`     | null                                        |

Pour plus d'information (détails & types spéciaux) : https://dart.dev/guides/language/language-tour#built-in-types

### Tableaux

```dart
var voitures = ["Saab", "Volvo", "BMW"];         //Avec données
const jeux = [];                                 //Sans données

//Ajout de données (correct même si const, car jeux est un objet qui ne change pas)
jeux[0] = 'Skyrim';
jeux[1] = 'The Witcher III : The Wild Hunt';
jeux[2] = 'tamere : la pute'

//pas correct car on change l'objet (devrait être var)
jeux = ['Skyrim', 'The Witcher III : The Wild Hunt', 'tamere : la pute'];
```

### Différences entre const et final

Pour faire simple, voyez `const` comme un `#define` de C++, il doit avoir une valeur à la déclartion et la variable sera simplement remplacer par sa valeur à la compilation.

`final` est une variable qui ne peut pas recevoir une nouvelle valeur une fois assignée.

**Note:** On n'est pas donc pas obligé d'assigner une valeur sur déclaration à une variable final

```dart
const a;     // Erreur: const doit avoir une valeur
const b = 2; // Correct
b = 4;       // Erreur: constante

final c; // Correct
c = 3;   // Correct
c = 10;  // Erreur: la variable à déja une valeur

```

## Blocs conditionnels

```dart
//If
if (year >= 2001) {
    print('21st century');
}
else if (year >= 1901) {
    print('20th century');
}
else {
    print('Vieux');
}

//Inline if
var nom = year >= 2001 ? '21st century' : 'Vieux';

//Switch
var status = 'OUVERT';
switch(status) {
    case 'OUVERT':
        print('Youpi!');
        break;
    default:
        print('Chouuuuuu');
}
```

## Boucles

```dart
//Foreach
for (final object in flybyObjects) {
  print(object);
}

//For
for (int month = 1; month <= 12; month++) {
  print(month);
}

//While
while (year < 2016) {
  year += 1;
}

//Do-While
do {
    year += 1;
} while (year < 2016);
```

## Fonctions

La syntaxe ressemble beaucoup celle de C++

```dart
int fibonacci (int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```
