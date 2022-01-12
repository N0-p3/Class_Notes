# Théorie
## Définition Générale
MongoDB est un SGBD orienté document ce qui signifie qu'il n'y à pas de SQL n'y de réelle structure dans une collection (table), cette dernière dépend de ce que nous, administrateur de BD, mettons à l'intérieur. Pensez y un peu comme à un document qui contient du JSON mais dans lequel on peut, à l'aide de fonctions, accéder au contenu et faire les opérations du CRUD. 
## Syntaxe
Non seulement la syntaxe utilisée pour la gestion d'une base de donnée est semblable à des appels de fonctions mais en plus, les données entrées dans un BD mongoDB sont très semblable, syntaxiquement parlant, à des objets javascript (ou JSON). Voici un exemple : 
```
db.users.insertOne({name: "John",  age: 30})
```
**PS** : Ceci insert un document dans la collections "users".
## Structure
La structure d'une collection dans mongoDB est lousse, et même très lousse. Ce que je veux dire par la c'est qu'avec mongoDB nous ne devons pas définir de colonnes ou de type de donnée qui ira dans un document. Un document est un entité à part entière qui contient les données qui lui sont spécifié et le seul lien entre lui et les autre document est sa collection. 
<br><br>
Donc il n'y à aucune structure, contrairement aux tables de SGDB conventionnelles, il n'y à pas de moules dans lequel chaque enregistrement doit "fitter", les données sont lousse dans la collection. Ceci signifie donc que on peut avoir des documents qui n'ont aucun champ en commun dans une même collection.
<br><br>
Additionnellement, une clef primaire, nommé "ObjectId", est associé à chaque document sans que nous aillons besoin de le spécifier. C'est comme ça par défaut.

## Terminologie
Voici la liste des termes utilisé dans le SGBD mongoDB :
| Mot           | Description                                                        |
|---------------|--------------------------------------------------------------------|
| Base de donné | Conteneur de collections.                                          |
| Collection    | Un groupe de document dans une base de donné (Table).              |
| Document      | Un enregistrement à l'intérieur d'une collection (Enregistrement). |
| Champ         | Une donné dans un document (Colonne).                              |