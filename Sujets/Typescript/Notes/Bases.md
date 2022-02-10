# Données et variables

## Types primitifs

Les types dans Typescript sont optionnel MAIS inférés ce qui signifie que si on met une String dans un variable, Typescript comprend que la variable à la type de String et donc on ne peux pas mettre autre chose que des Strings. Voici la syntaxe de déclaration de variables avec des types en plus d'un exemple démontrant tout les types primitifs :

```typescript
let a: number = 5;        												// Int / Float
let b: string = 'tamere';												// String
let c: boolean = true;    												// Boolean
let d: any = 'whatever';												// Peux être n'importe quoi et peux changer de type

let e: number[] = [1,2,3,4,5];											// Tableau de Number
let f: any[] = [true, 1, 2, 3, 'tamere', { name : 'tamere', age : 69 }]	// Tableau de Any
```

**Note** : Évidemment, on peux séparer l'instanciation de l'assignation.
  
## Tuple

Les Tuples sont en gros des paires (de 2 et 3 et surment plus) de données qui ont exactement les types de données spécifiés dans eux. C'est comme un tableau mais avec des types spécifiques dans un ordre spécifique. Voici un exemple :

```typescript
let person: [string, number, boolean] = ['tamere', 69, true];
```

Si on tente de mettre autre chose que une String, un nombre et un Boolean (dans cet ordre) dans le tuple, il voudra pas, y va pas aimer ça! <br><br>

Il est aussi possible de faire des tableaux de Tuple en ajoutant les `[]` après notre Tuple! Voici la syntaxe : 

```typescript
let desTuples: [number, string, boolean, any][];
```

## Union

Ce que Typescript appel les Unions sont en fait une variable capable d'être un type ou un autre, il peux changer entre les deux à tout moment. C'est comme si une variable avait deux types. Voici la syntaxe : 

```typescript
let bi: number | string = 'tamere';
bi = 480;
```

## Enum

Typescript apporte aussi les Énums! Je vais juste vous montrer la syntaxe parce que... bein on sait tous c'est quoi un Énum :

```typescript
enum directions {
	Up,
	Down,
	Left,
	Right
}
```
**Note** : Vous pouvez définir les valeurs dans l'énum par vous même en mettant un égal et en donnant une valeur à un des éléments (comme ça : `Up = 1,`). <br>
**Note** : Les types valide dans les Énums sont les `number` et les `string`. <br>
**Note 2** : Si vous souhaitez que votre énum commence à un autre chiffre que 0 vous pouvez seulement changer la valeur du premier élément dans l'énum et Typescript va comprendre et donné la bonne valeur autre chiffre après (si yer tu pas intelligent!).

## Affirmation de types (Type assertion)

L'affirmation de types sert un peu à "caster" une variable, c'est une façon de dire au système : "yo man, je veux que tu considère que ste variable là est de tel type." ce qui est franchement très proche du casting mais pas exactement, vue qu'elle ne fonctionne qu'avec les Unions (pas super bien) et les variable de type `any` (fonction bien). <br><br>

Donc ce qui ce passe avec l'affirmation de type d'une variable `any` c'est que peu importe ce que la variable contient, y va essayer de son mieux pour "assert" la variable en le type qu'on lui demande (on garantis pas le résultat mais Typescript chiale pas). <br>
Par contre, pour les Unions, c'est différent. Si on à un Union qui contient en ce moment un `number` et qu'on le "assert" en `number` ça va fonctionner, mais si il se trouve à être de son autre type, la Typescript va chialer (fouille moi pourquoi).<br><br>

Bref, voici la syntaxe :

```typescript
let id: any = 1;

let customerId: number = <number>id;	// Manière #1
let customerId: number = id as number	// Manière #2
```

# Fonction

Afin de définir une fonction, la syntaxe est exactement pareil à Javascript mais on spécifi les types dans les parenthèses en plus de sp/cifier la valeur de retour après les paramètres :

```typescript
function sum(a: number, b: number): number {
	return a + b;
}
```

**Note** : Si on veux que notre fonction retourne rien on peux le spécifier en mettant `void` dans la valeur de retour (dans la signature de la fonction).
**Note 2** : On peux aussi avoir des Unions en tant que paramètre d'une fonction.

## Générique (template)

Les génériques sont une façon de créer un bout de code réutilisable dépendament de la situation. Disons que nous voulons qu'une fonction nous retourne un tableau avec un type que nous ne voulons pas prédéfinir (pour faire en sorte que cette fonction sois réutilisable et pour par avoir à faire plusieurs fonctions qui font la même chose) nous allons utilisé un générique. Voici un exemple :

```typescript
function getArray<T>(items: T[]): T[] {
	return new Array().concat(items);
}

let numArray = getArray<number>([1, 2, 3, 4, 5]);
```

Donc avec les génériques on peux créer du code plus souple qui permet de faire plus de choses tout en restant stricte (en utilisant un type primitif et non `any`).

# Type (struct)

La façon que Typescript gère les objets (sans classes) est en créant ce que Typescript appel des "types" (essentiellement c'est un objet mais eux y appelent ça de même). Donc pour ce créer un objet (un peu comme une "struct", sans méthodes) on va dabord se créer un type et ensuite on va en faire des objets. Voici la syntaxe pour créer un type :

```typescript
type Person = {				// Le type
	name: string,
	age: number, 
	sex: boolean
}

const person: Person = {	// Instanciation faisant usage du type Person
	name: 'Paul',
	age: 23,
	sex: false
}
```

# Classe

Les classes en Typescript sont exactement pareil aux classes dans Javascript MAIS elles ont des types, donc voici l'exemple dans les notes de Node.js en Typescript : 

```typescript
class Person {
    name: string;
    age: number;
    sex: boolean;

    constructor(name: string, age: number, sex: boolean) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }

    makeOlder(years: number) {
        this.age += years;
    }
}
```

L'instanciation est pareil : 

```typescript
let tamere = new Person('tamere', 69, true);
```

## Modificateur de propriété

Par défaut, les propriétés dans une classe sont publiques mais on peux changer çela en précisant le niveau d'accès d'une propriété en mettant `protected`, `private` ou `public` (si on veux être plus implicite) devant.

```typescript
class Employee {
    protected id: number;
    name: string;
    age: number;
    private sex: boolean;

    constructor(id: number, name: string, age: number, sex: boolean) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
}
```

# Interface

Les interfaces dans Typescript servent de définition (ou de moule) à un objet ET à une classe (si on le souhaite) avec quelque fonctionnalités de plus qu'un Type. Voici la syntaxe :

```typescript
interface PersonInterface {						// Interface
    name: string,
    age: number,
    sex: boolean
}

const p: PersonInterface = { 					// Instanciation d'un objet à partir de l'interface 
	name: 'tamere',
	age: 69,
	sex: true
}

class Employee implements PersonInterface {		// Implémentation de l'interface dans une classe
    name: string;
    age: number;
    sex: boolean;

    constructor(name: string, age: number, sex: boolean) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
}
```

## Modificateurs de propriétés

Il est possible de spécifier qu'un propriété n'est pas obligatoire avec `?` ou de permettre la lecture d'un propriété uniquement avec `readonly` ainsi :

```typescript
interface EmployeeInterface {
    readonly id: number,		// readonly
	name: string,
    age: number,
    sex?: boolean				// propriété non-obligatoire
}
```

## Fonctions d'interface

Il est aussi possible de spécifier des signatures de fonctions dans un interface ainsi : 

```typescript
interface PersonInterface {
    name: string,
    age: number,
    sex: boolean

    makeOlder(years: number): void
}
```