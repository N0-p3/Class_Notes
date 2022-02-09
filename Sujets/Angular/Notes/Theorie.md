# Angular c'est quoi?

À venir.

# Terminologie

## Module

Un module est un ensemble de composant dans Angular qui se retrouve tous sous un même thème ou une même section, par exemple un module de connexion pourrait avoir plusieur composants qui forme la vue et les fonctionnalité du module de connexion et permet (evidement) la connexion d'un client.

**Note** : Le module app est le module racine de tout projet.

## Composant

Un composant un élément dans Angular qui est fortement liée à la vue, qui gère son style (apparence au frontend) et ses actions (donc elle à un contrôleur avec des fonctions et etc.). C'est un peu comme une classe Typescript qui à une vue rattaché à elle et le tout représente un composant du plus petit au plus grand (un simple bouton jusqu'à une page complète).

## Service

Un service est un élément dans Angular qui est fortement liée au backend, par exemple : requète fetch, Journalisation des événements, la gestion des messages d'alertes et etc.

# Normes Angular

## Responsabilité unique

- Un fichier se limite à un seul concept (composant, service ou modèle).
- Un fichier se limite à 400 lignes de code (aéré).
- Une fonction se limite à 75 lignes de code.
- Un dossier ne peux contenir plus de 7 fichiers.

Le principe est de ne pas avoir à documenter ou à commenter le code, on préfère diviser celui-ci pour éviter la complexité, limiter les bugs et permettre une réutilisation de code la plus optimale. Si jamais un des vos fichier (que ce soit un module, composant ou un service) dépasse ces limites, c'est qu'il peut (et doit) être diviser en plusieurs autres sous-éléments. 

## Nomenclature des fichiers

- Les fichiers doivent suivre le template de nomenclature suivant : <fonctionnalité>.<type>.ts. Exemple : login.component.ts .
- Si un nom de component comporte une espace, remplacez celle-ci par un tiret ("-"). Exemple : users-list.component.ts .
- Ne pas utiliser d'abréviation dans les nom d'éléments.
- Le nom des classes est en UpperCamelCase. Exemple : le fichier "users-list.component.ts" contiendra la classe "UsersListComponent".
  - Les services qui ont un verbe comme nom, (exemple : "logger.service.ts") peut contenir la classe "Logger" au lieu de "LoggerService".

## Pourquoi ces normes?

Ces normes ont été établies afin de faire respecter le LIFT qui se défini comme :

- **Locate code quickly**                   (Trouver rapidement le code).
- **Identify the code at a glance**         (Identifier le code d'un coup d'oeil).
- **Keep the Flattest structure you can**   (Garder une structure plate).
- **Try to be DRY**                         (Essayer d'être DRY (Don't Repeat Yourself)).


# Commandes utiles

| Commandes                           | Commandes courtes    | Descriptions                  |
|-------------------------------------|----------------------|-------------------------------|
| ng generate module modulePath       | ng g m modulePath    | Génération de module.         |
| ng generate component componentPath | ng g c componentPath | Génération de composants.     |
| ng generate service servicePath     | ng g s servicePath   | Génération de service.        |
| ng generate class classPath         | ng g cl classPath    | Génération de classe.         |
| npm start                           | npm start            | Exécute le "serveur" Angular. |
| npm build                           | npm build            | Compile le projet Angular.    |


# Installation 

1. Assurez-vous d'avoir npm d'installé (ce qui devrait être fait si vous avez installé Node.js).
2. Installer Angular avec : `sudo npm i -g @angular/cli`.
3. Confirmer que tout est bien installer avec : `ng -v`

# Setup Angular

Pour initialiser Angular, il suffit de rouler la commande suivante dans votre dossier qui contiendera Angular :

```
ng new -S -g --directory ./ang projectName
```

**Note** : -S skip tout ce qu'on à besoin pour faire des tests, -g skip la création du git et --directory sert à spécifier ou on installe Angular et on lui passe le nom du projet.

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