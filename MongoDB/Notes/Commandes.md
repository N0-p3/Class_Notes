# Commandes
## Commandes de bases
Voici les commandes de bases et une description de ce qu'elle font :
| Commande          | Description                                                                                                                           |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| show dbs          | Montre les toutes les bases de données.                                                                                               |
| show collections  | Montre toutes les collections (tables).                                                                                               |
| use dbName        | Définit la base de données spécifiée comme étant la base de données active OU créer la base de données si celle-ci n'existe pas déjà. |
| db                | Montre la base de données utilisée en ce moment.                                                                                      |
| db.collectionName | Accéder à la collection spécifier ou créer la collection si celle-ci n'existe pas déjà.                                               |
| db.dropDatabase() | Supprime la base de données utilisée en ce moment.                                                                                    |
| cls               | Nettoie l'écran.                                                                                                                      |
| exit              | Quitte mongosh.                                                                                                                       |

**Note** : Dans les sections suivante il se peut que je parle d'"objet" qui sont en fait des documents, je les nommes ainsi puisque leur syntaxe est exactement pareil à celle d'un objet JSON ou JS (comme précisé précédement dans la [section théorique](./Theorie.md#Syntaxe)).<br>
## Create
Voici les commandes servant à la création de collections et de documents (en bref) :
| Exemple de commande                                  | Description                                 |
|------------------------------------------------------|---------------------------------------------|
| `db.collection.insertOne({object})`                  | Insert un seul objet dans la collection.    |
| `db.collection.insertMany([object, object, object])` | Insert plusieurs objets dans la collection. |

**Note** : Veuillez remplacer "collection" par la collection appropriée dans votre cas et veuillez remplacer les occurences de "objet" par les objets nécéssaire.
<br><br>
Lorsque l'on ajoute un document à une collection, un objet peux contenir plusieurs données (évidemment), des tableaux et d'autre objets. Voici un exemple qui fait exactement ces trois choses :

```
db.users.insertOne({
    name: 'Nycola',
    age: 19, 
    hobbies: ['Gaming', 'Weight lifting', 'Programming', 'StuDYING'], 
    address: {
        city: 'Montréal', 
        zipCode: 'H1A1A1', 
        street: 'rue Victoria', 
        addressNumber: 123
    }
})
```
## Read
Voici les commandes servant à la lecture de collections et de documents : 
| Commandes                                             | Description
|-------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| `db.collection.find()`                                | Affiche toutes les données. |                                                  
| `db.collection.findOne()`                             | Affiche le premier document qui correspond à la recherche du `findOne()`. |
| `db.collection.find().limit(n)`                       | Limite le résultat du `find()` à n résultat (n étant un nombre). |
| `db.collection.find().sort({data: 1 / -1})`           | Affiche le résultat du `find()` en ordre spécifier (1 = croissant / alphabétique, -1 = décroissant / alphabétique inversé) de la `data`. |
| `db.collection.find().skip(n)`                        | Affiche le résultat du `find()` en ignorant n résultat (n étant un nombre). |
| `db.collection.find({ data: value })`                 | Affiche le résultat du `find()` en filtrant avec un objet. |
| `db.collection.find({ data: value }, {data: 1 / 0 })` | Affiche le résultat du `find()` en filtrant avec un objet et en spécifiant quelles champs on veux des documents résultat du `find()` (1 = affiche moi ce champ, 0 = affiche moi pas ce champ). |
| `db.collection.find({ data: filterObject })`          | Affiche le résultat du `find()` en filtrant avec un objet de filtre. |

**Note** : Les fonctions peuvent être "stacker" une par dessus l'autre si nécéssaire.
**Note 2** : Il est possible d'utiliser la fonction `sort()` avec plusieurs données (ce qui va trier les données dans l'ordre dans laquelle elles sont écrite).<br>
**Note 3** : Lorsque l'on filtre avec un objet, c'est comme si on demandais de nous sortir tout les objets qui on les données que nous y passons. <br>
**Note 4** : Lorsque l'on filtre avec un objet **ET** que l'on spécifie les champs que l'on veux, si on spécifie juste un champ positivement (donc on veux qu'il nous le donne, on a mit un 1) **SEULEMENT** ce champ sera retourné. Dans le cas contraire, si on spécifie un champ négativement (donc on ne veux pas le champ, on a mit un 0) **SEULEMENT** ce champs sera ignoré (tout les autres seront présent). Finalement si nous mettons des deux type de modificateur de présence de champ (1 ou 0) il fera exactement cela, montrera ceux qui sont a 1 et par ceux qui sont à 0. De plus, 0 et 1 peuvent être remplacer par `false` et `true`.

### Objet de filtre
Voici les différents objets de filtres disponible avec mongoDB :
| Objet de filtre                        | Signification      | Description
|----------------------------------------|--------------------|---------------------------------------------------------------------------------------| 
| `{ $eq: value }`                       | equal              | Vérifie si le champ auquel cet objet est comparé est égal à `value`.                  |
| `{ $ne: value }`                       | not equal          | Vérifie si le champ auquel cet objet est comparé n'est pas égal à `value`.            |
| `{ $gt: value }`                       | greater            | Vérifie si le champ auquel cet objet est comparé est plus grand que `value`.          |
| `{ $gte: value }`                      | greater or equal   | Vérifie si le champ auquel cet objet est comparé est plus grand ou égal à `value`.    |
| `{ $lt: value }`                       | less than          | Vérifie si le champ auquel cet objet est comparé est plus petit que `value`.          |
| `{ $lte: value }`                      | less than or equal | Vérifie si le champ auquel cet objet est comparé est plus petit ou égal à `value`.    |
| `{ $in: [value, value, value] }`       | in                 | Vérifie si le champ auquel cet objet est comparé est pareil a un des `value`.         |
| `{ $nin: value }`                      | not in             | Vérifie si le champ auquel cet objet est comparé n'est pas pareil à un des `value`.   |
| `{ $and: [data: value, data: value] }` | and                | Vérifie si plusieurs conditions (objets de filtre) sont tous vrais.                   |
| `{ $or: [data: value, data: value] }`  | or                 | Vérifie si au moins une des conditions (objet de filtre) soit vrais.                  |
| `{ $not: value }`                      | not                | Vérifie si le champ auquel cet objet est comparé n'est pas `value`. (semblable à $ne) |
| `{ $exists: true / false }`            | exists             | Vérifie si le champ auquel cet objet est comparé existe (ou pas, dépendant du bool).  |
| `{ $expr: filterObject }`              | expression         | Effectue une comparaison entre deux champs dépendant de l'objet filtre passé.         |

#### Exemple d'usage d'objet de filtre
## Update
## Delete