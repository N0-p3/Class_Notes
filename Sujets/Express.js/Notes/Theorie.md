# Express.js c'est quoi?

Donc en gros, Express.js c'est un framework Javascript "back-end" qui sert à faire tout ce qui est lié à un serveur : Hébergement de site web, API, communication à une base de donnée, système server-client et etc. Ce framework est comme un bloc rajouter par dessus Node.js pour gerer tout ce qui est lié à un serveur. Express.js est très populaire dans sa catégorie et est très performant, minimaliste et léger. De plus, Express.js est très souple et léger, ce que j'entend par là c'est qu'il permet de développer une application web sans moule pré-fait dans lequel ya déja un million de fichiers générés par 480 paquets importé par le framework, donc en gros, il permet au développeur de se faire sa propre architecture d'application comme il le souhaite (pas comme un framework vraiment laid, horrible et maudit *TOUSSE TOUSSE* YII *TOUSSE TOUSSE*). <br><br>

En plus, Express.js offre des fonctions de Middleware ce qui permet d'éxecuter du code avant et après certaines étapes de l'éxécution d'une certaine tache (comme vue précédemment dans [Mongoose](../../Mongoose/Notes/Bases.md#middleware-de-schéma))!

# Installation

## Windows

Pour mes misérables utilisateurs Windows :

1. Assurez-vous d'avoir npm d'installé (ce qui devrait être fait si vous avez installé Node.js).
2. Déplacer vous dans le dossier de votre projet.
3. Créer votre fichier Javascript de serveur (point d'entré).
4. (**OPTIONEL SI DÉJÀ FAIT**) Initiliser npm avec : `npm init -y`.
5. Exécutez la commande suivante `npm i express --save` dans un terminal (PAS POWERSHELL).
6. Assurez-vous que le `"main"` est bien votre point d'entré (du serveur) dans le `package.json`. 

## Linux

Pour mes chers utilisateur Linux :

1. Assurez-vous d'avoir npm d'installé (ce qui devrait être fait si vous avez installé Node.js).
2. Déplacer vous dans le dossier de votre projet.
3. Créer votre fichier Javascript de serveur (point d'entré).
4. (**OPTIONEL SI DÉJÀ FAIT**) Initiliser npm avec : `npm init -y`.
5. Exécutez la commande suivante `sudo npm i express --save` dans une console.
6. Assurez-vous que le `"main"` est bien votre point d'entré (du serveur) dans le `package.json`. 