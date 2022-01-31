# Définition Générale

MongoDB est un SGBD orienté document ce qui signifie qu'il n'y à pas de SQL n'y de réelle structure dans une collection (table), cette dernière dépend de ce que nous, administrateur de BD, mettons à l'intérieur. Pensez y un peu comme à un document qui contient du JSON mais dans lequel on peut, à l'aide de fonctions, accéder au contenu et faire les opérations du CRUD. 

# Syntaxe

Non seulement la syntaxe utilisée pour la gestion d'une base de donnée est semblable à des appels de fonctions mais en plus, les données entrées dans un BD mongoDB sont très semblable, syntaxiquement parlant, à des objets javascript (ou JSON). Voici un exemple : 
```
db.users.insertOne({name: "John",  age: 30})
```
**PS** : Ceci insert un document dans la collections "users".

# Structure

La structure d'une collection dans mongoDB est lousse, et même très lousse. Ce que je veux dire par la c'est qu'avec mongoDB nous ne devons pas définir de colonnes ou de type de donnée qui ira dans un document. Un document est un entité à part entière qui contient les données qui lui sont spécifié et le seul lien entre lui et les autre document est sa collection. 
<br><br>
Donc il n'y à aucune structure, contrairement aux tables de SGDB conventionnelles, il n'y à pas de moules dans lequel chaque enregistrement doit "fitter", les données sont lousse dans la collection. Ceci signifie donc que on peut avoir des documents qui n'ont aucun champ en commun dans une même collection.
<br><br>
Additionnellement, une clef primaire, nommé "ObjectId", est associé à chaque document sans que nous aillons besoin de le spécifier. C'est comme ça par défaut.

# Terminologie

Voici la liste des termes utilisé dans le SGBD mongoDB :
| Mot           | Description                                                        |
|---------------|--------------------------------------------------------------------|
| Base de donné | Conteneur de collections.                                          |
| Collection    | Un groupe de document dans une base de donné (Table).              |
| Document      | Un enregistrement à l'intérieur d'une collection (Enregistrement). |
| Champ         | Une donné dans un document (Colonne).                              |

# Installation

Afin d'installer mongoDB et de pouvoir jouer avec ce merveilleux SGBD, il va nous falloir deux choses : MongoDB et mongosh. MongoDB est l'engin relationnel, toute la patente de BD, de MongoDB et mongosh est un programme console qui permet d'intéragir avec MongoDB. Je vous conseil fortement d'aller vous même voir sur le site officiel de MongoDB puisque les informations ici sont très minime.
Voici le lien pour [MongoDB](https://docs.mongodb.com/manual/installation/) et pour [mongosh](https://docs.mongodb.com/mongodb-shell/install/)

## Windows

Pour l'installation sous Windows, le tout est infiniement simple : 
1. Dirigez vous sur le site web de documentation de [MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/).
2. Téléchargez l'[installateur](https://www.mongodb.com/try/download/community?tck=docs_server&_ga=2.101412997.507167780.1642204555-631246763.1641858718) de mongoDB.
3. Exécuter et suivez les étapes de l'installateur.
4. Téléchargez l'[installateur](https://www.mongodb.com/try/download/shell?jmp=docs&_ga=2.130192651.507167780.1642204555-631246763.1641858718) de mongosh.
5. Exécuter et suivez les étapes de l'installateur.

## Linux 

Pour l'installation sous Linux :
1. Dirigez vous sur le site web de document de [MongoDB](https://docs.mongodb.com/manual/installation/) (ce lien est différent que celui de Windows).
2. Sélectionnez votre distribution dans la table en haut de page.
3. Suivez les étapes indiqués.

### Ubuntu

1. Importer la clef publique GPG de MongoDB : `wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -`.
2. Créer le fichier liste pour MongoDB : `echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list`
3. Recharger la base de donnée local des paquets : `sudo apt update`
4. Installer MongoDB et mongosh : `sudo apt install -y mongodb-org mongodb-mongosh`

# Lancer le service

Afin de lancer le service sous Linux, exécutez : `sudo systemctl start mongod`.