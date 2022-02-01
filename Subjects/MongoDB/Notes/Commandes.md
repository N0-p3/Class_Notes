# Commandes de bases

Voici les commandes de bases et une description de ce qu'elle font :

| Commande             | Description                                                                                                                           |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| show dbs             | Montre les toutes les bases de données.                                                                                               |
| show collections     | Montre toutes les collections (tables).                                                                                               |
| use dbName           | Définit la base de données spécifiée comme étant la base de données active OU créer la base de données si celle-ci n'existe pas déjà. |
| db                   | Montre la base de données utilisée en ce moment.                                                                                      |
| db.collectionName    | Accéder à la collection spécifier ou créer la collection si celle-ci n'existe pas déjà.                                               |
| db.dropDatabase()    | Supprime la base de données utilisée en ce moment.                                                                                    |
| db.collection.drop() | Supprime la collection spécifié.                                                                                                      |
| cls                  | Nettoie l'écran.                                                                                                                      |
| exit                 | Quitte mongosh.                                                                                                                       |

**Note** : Dans les sections suivante il se peut que je parle d'"objet" qui sont en fait des documents, je les nommes ainsi puisque leur syntaxe est exactement pareil à celle d'un objet JSON ou JS (comme précisé précédement dans la [section théorique](./Theorie.md#Syntaxe)).

# Create

Voici les commandes servant à la création de collections et de documents (en bref) :
| Exemple de commande                                  | Description                   |
|------------------------------------------------------|-------------------------------|
| `insertOne({object})`                  | Insert un seul objet dans la collection.    |
| `insertMany([object, object, object])` | Insert plusieurs objets dans la collection. |

**NOTE IMPORTANTE** : Les commandes dans ce document-ci, présent sous vous merveilleux petits yeux, se doivent d'être écrite suivant la légende suivante : `db.<nomCollection>.<commande>` et veuillez remplacer les occurences de "objet" par les objets nécéssaire.
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

# Read

Voici les commandes servant à la lecture de collections et de documents : 
| Commandes                               | Description                                                                                                                                                           |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `find()`                                | Affiche toutes les données.                                                                                                                                           |
| `countDocuments()`                      | Affiche le nombre de documents dans la collection.                                                                                                                    |
| `countDocuments({object})`              | Affiche le nombre de documents correspondant aux conditions indiqués dans l'objet.                                                                                    |
| `findOne()`                             | Affiche le premier document qui correspond à la recherche du `findOne()`.                                                                                             |
| `find().limit(n)`                       | Limite le résultat du `find()` à n résultat (n étant un nombre).                                                                                                      |
| `find().sort({data: 1 / -1})`           | Affiche le résultat du `find()` en ordre spécifier (1 = croissant / alphabétique, -1 = décroissant / alphabétique inversé) de la `data`.                              |
| `find().skip(n)`                        | Affiche le résultat du `find()` en ignorant n résultat (n étant un nombre).                                                                                           |
| `find({ data: value })`                 | Affiche le résultat du `find()` en filtrant avec un objet.                                                                                                            |
| `find({'object.data': value})`          | Affiche le résultat du `find()` en filtrant par le contenu d'un champ dans un objet d'un document. `'object.data'` est comme tout autre champ dans le document        | 
| `find({ data: value }, {data: 1 / 0 })` | Affiche le résultat du `find()` en filtrant avec un objet et en spécifiant quelles champs on veux des documents résultant du `find()` (1 = affiche, 0 = affiche pas). |
| `find({ data: filterObject })`          | Affiche le résultat du `find()` en filtrant avec un objet de filtre.                                                                                                  |

**Note** : Les fonctions peuvent être "stacker" une par dessus l'autre si nécéssaire.<br>
**Note 2** : Il est possible d'utiliser la fonction `sort()` avec plusieurs données (ce qui va trier les données dans l'ordre dans laquelle elles sont écrite).<br>
**Note 3** : Lorsque l'on filtre avec un objet, c'est comme si on demandais de nous sortir tout les objets qui on les données que nous y passons. <br>
**Note 4** : Lorsque l'on filtre avec un objet **ET** que l'on spécifie les champs que l'on veux, si on spécifie juste un champ positivement (donc on veux qu'il nous le donne, on a mit un 1) **SEULEMENT** ce champ sera retourné. Dans le cas contraire, si on spécifie un champ négativement (donc on ne veux pas le champ, on a mit un 0) **SEULEMENT** ce champs sera ignoré (tout les autres seront présent). Finalement si nous mettons des deux type de modificateur de présence de champ (1 ou 0) il fera exactement cela, montrera ceux qui sont a 1 et par ceux qui sont à 0. De plus, 0 et 1 peuvent être remplacer par `false` et `true`.

# Update

Voici les commandes servant à la mise à jour de documents :
| Commandes                                   | Description                                                                                                   |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `updateOne({data: value}, modifierObject)`  | Modifie le premier document qui correspond à la recherche (premier paramètre) selon l'objet de mise à jour.   |
| `updateMany({data: value}, modifierObject)` | Modifie tous les documents qui correspondent à la recherche (premier paramètre) selon l'objet de mise à jour. |
| `replaceOne({data: value}, object)`         | Remplace le premier document qui correspond à la recherche (premier paramètre) par le second objet passé.     |

**Note** : Lorsque l'on veux faire une mise à jour sur tout les documents, il suffit de faire un `updateMany()` avec le premier paramètre vide, comme ça : `db.<nomCollection>.updateMany({}, modifierObject)`.

# Delete

**Note** : les commandes des opérations dans cette section fonctionnent **EXACTEMENT** comme le `find()` mais supprime ce qu'elle trouve au lieu de l'imprimer à l'écran.
Voici les commandes servant à la suppression de documents :
| Commandes                   | Description                                          |
|-----------------------------|------------------------------------------------------|
| `deleteOne({data: value})`  | Supprime le premier document qui match la recherche. |
| `deleteMany({data: value})` | Supprime tous les documents qui match la recherche.  |

# Objet de mise à jour

Voici les différents objets de mise à jour disponible avec mongoDB :
| Objet de mise à jour         | Description                                                   |
|------------------------------|---------------------------------------------------------------|
| `{$set: {data: value}}`      | Met à jour les champs passés à l'objet de mise à jour.        |
| `{$inc: {data: value}}`      | Incrémente le champ numérique `data` de la valeur de `value`. |
| `{$rename: {data: 'value'}}` | Renomme le nom du champ `data` pour `value`.                  |
| `{$unset: {data: ''}}`       | Enlève le champ `data` du document.                           |
| `{$push: {data: value}}`     | Ajoute `value` au tableau `data`.                             |
| `{$pull: {data: value}}`     | Enlève `value` au tableau `data`.                             |

**Note** : Si on "push" sur un tableau qui n'existe pas, le tableau sera créer.

## Exemple d'usage d'objets de mise à jour

Voici des exemples d'usage des objets de mise à jour :
| Objet de mise à jour | Exemple                                                                                     | Description                                                                               |
|----------------------|---------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| `$set`               | `db.users.updateOne({_id: ObjectId('61df7434aa581c6f1eabc480')}, {$set: {name: 'Robert'}})` | Change le champ `name` du document dont l'id est '61df7434aa581c6f1eabc480' pour 'Robert' |
| `$inc`               | `db.users.updateOne({age: 12}, {$inc: {age: 2}})`                                           | Incrémente le champ `age` de la valeur de 2 pour le premier document trouvé.              |
| `$rename`            | `db.users.updateMany({}, {$rename: {age: 'level'}})`                                        | Renomme le nom du champ `age` pour 'level' pour tout les documents.                       |
| `$unset`             | `db.users.updateOne({age: 12}, {$unset: {age: ''}})`                                        | Enlève le champ `age` du premier document trouvé.                                         |
| `$push`              | `db.users.updateMany({}, {$push: {friends: 'George'}})`                                     | Ajoute 'George' au tableau `friends` pour tout les utilisateurs.                          |
| `$pull`              | `db.users.updateMany({}, {$pull: {friends: 'Nathaniel'}})`                                  | Enlève 'Nathaniel' au tableau `friends` pour tout les utilisateurs.                       |

# Objet de filtre

Voici les différents objets de filtres disponible avec mongoDB :
| Objet de filtre                        | Signification      | Description                                                                                   |
|----------------------------------------|--------------------|-----------------------------------------------------------------------------------------------| 
| `{ $eq: value }`                       | equal              | Vérifie si le champ auquel cet objet est comparé est égal à `value`.                          |
| `{ $ne: value }`                       | not equal          | Vérifie si le champ auquel cet objet est comparé n'est pas égal à `value`.                    |
| `{ $gt: value }`                       | greater            | Vérifie si le champ auquel cet objet est comparé est plus grand que `value`.                  |
| `{ $gte: value }`                      | greater or equal   | Vérifie si le champ auquel cet objet est comparé est plus grand ou égal à `value`.            |
| `{ $lt: value }`                       | less than          | Vérifie si le champ auquel cet objet est comparé est plus petit que `value`.                  |
| `{ $lte: value }`                      | less than or equal | Vérifie si le champ auquel cet objet est comparé est plus petit ou égal à `value`.            |
| `{ $in: [value, value, value] }`       | in                 | Vérifie si le champ auquel cet objet est comparé est pareil a un des `value` dans le tableau. |
| `{ $nin: value }`                      | not in             | Vérifie si le champ auquel cet objet est comparé n'est pas pareil à un des `value`.           |
| `{ $and: [data: value, data: value] }` | and                | Vérifie si plusieurs conditions (objets de filtre) sont tous vrais.                           |
| `{ $or: [data: value, data: value] }`  | or                 | Vérifie si au moins une des conditions (objet de filtre) soit vrais.                          |
| `{ $not: filterObject }`               | not                | Vérifie si le champ auquel cet objet est comparé n'est pas `value`. (semblable à $ne)         |
| `{ $exists: true / false }`            | exists             | Vérifie si le champ auquel cet objet est comparé existe (ou pas, dépendant du bool).          |
| `{ $expr: filterObject }`              | expression         | Effectue une comparaison entre deux champs dépendant de l'objet filtre passé.                 |

## Exemple d'usage d'objets de filtre

Voici des exemples d'usage des objets de filtre avec `find()` : 
| Objet de filtre | Exemple                                                    | Description                                                                        |
|-----------------|------------------------------------------------------------|------------------------------------------------------------------------------------|
| `$eq`           | `db.users.find({ name : { $eq: 'Kyle' }})`                 | Retourne tout les utilisateurs avec le nom de 'Kyle'.                              |
| `$ne`           | `db.users.find({ name: { $ne: 'Kyle' }})`                  | Retourne tout les utilisateurs qui n'ont pas le nom de 'Kyle'.                     |
| `$gt`           | `db.users.find({ age: { $gt: 18 }})`                       | Retourne tout les utilisateurs qui on un age supérieur à 18.                       |
| `$gte`          | `db.users.find({ age: { $gte: 18 }})`                      | Retourne tout les utilisateurs qui on un age supérieur ou égal à 18.               |
| `$lt`           | `db.users.find({ age: { $lt: 18 }})`                       | Retourne tout les utilisateurs qui on un age inférieur à 18.                       |
| `$lte`          | `db.users.find({ age: { $lte: 18 }})`                      | Retourne tout les utilisateurs qui on un age inférieur ou égal à 18.               |
| `$in`           | `db.users.find({ name: { $in: ['Kyle', 'Mike'] }})`        | Retourne tout les utilisateurs dont le nom est 'Kyle' ou 'Mike'.                   |
| `$nin`          | `db.users.find({ name: { $nin: ['Kyle', 'Mike'] }})`       | Retourne tout les utilisateurs dont le nom n'est pas 'Kyle' ou 'Mike'.             |
| `$and`          | `db.users.find({ $and: [{ age: 12 }, { name: 'Kyle' }] })` | Retourne tout les utilisateurs dont l'age est de 12 et dont le nom est 'Kyle'.     |
| `$or`           | `db.users.find({ $or: [{ age: 12 }, { name: 'Kyle' }] })`  | Retourne tout les utilisateurs dont l'age est de 12 ou dont le nom est 'Kyle'.     |
| `$not`          | `db.users.find({ name: { $not: { $eq: 'Kyle' }}})`         | Retourne tout les utilisateurs dont le nom n'est pas 'Kyle'.                       |
| `$exists`       | `db.users.find({ name: { $exists: true }})`                | Retourne tout les utilisateurs dont le nom est un champ qui existe.                |
| `$expr`         | `db.users.find({ $expr: { $gt: ['$balance', '$dette'] })`  | Retourne tout les utilisateurs dont leur balance est plus grande que leurs dettes. |

**Note** : Lorsque l'on accède à la valeur d'une colonne il est important d'ajouter un `$` ainsi : `'$nomColonne'` comme dans l'exemple de `$expr`.

Il est possible de combiné les objets de filtre ainsi : 

```
db.users.find({age: {$gte: 20, lte: 40}}) //Retourne les utilisateurs entre 20 et 40 ans inclusivement
```

Cette Combinaison de filtre est l'équivalent de : celle-ci :

```
db.users.find({$and: [{age: {$gte: 20}}, {age: {$lte: 40}}]})
```