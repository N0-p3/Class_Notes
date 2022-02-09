# Setup d'un projet

Voici les étapes à suivre pour débuter un projet :

1. [Installer Node.js](../../Node.js/Notes/Theorie.md#installation).
2. [Installer MongoDB](../../MongoDB/Notes/Theorie.md#installation).
3. Créer votre dossier de projet.
4. Ouvrir un terminal à la racine du dossier.
5. Créer un fichier Javascript vide avec : `touch server.js`.
6. Initiliser npm avec : `sudo npm init -y`.
7. Installer Express.js avec : `sudo npm i express --save`.
8. Installer Mongoose avec : `sudo npm i mongoose --save`.
9. Créer un nouveau dossier dans lequel sera contenu Angular, exemple : `mkdir ./ang`
10. Installer Angular dans ce dernier dossier avec : `ng new -S -g --directory ./ang projectName`.
11. Répondre au questions de Angular selon les réponses recommandés.
12. Assurez-vous que le `"main"` est bien votre point d'entré (du serveur) dans le `package.json`.

**Note** : À l'étape 10, -S skip tout ce qu'on à besoin pour faire des tests, -g skip la création du git et --directory sert à spécifier ou on installe Angular et on lui passe le nom du projet.

## Questions Angular 

> Voulez-vous une vérification de type plus strict?

Défaut: Non <br>
**Recommandé** : Oui

> Voulez-vous ajouter le "routing" Angular?

Défaut: Non <br>
**Recommandé** : Absolument beaucoup OUI

> Quel format CSS voulez-vous utiliser?

Défaut: CSS <br>
**Recommandé** : SCSS

## Démarrage 

| Commandes | Définition                              |
|-----------|------------------------------------------|
| npm start | Démarrer Angular.                        |
| npm build | Compiler Angular, prêt à la publication. |
