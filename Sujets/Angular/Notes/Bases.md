# Composant

Un composant est fait de 4 fichiers (3 sans les tests) possédant tous des extensions différentes ainsi que des rôles différents, voici une description de ceux-ci : 

| Extensions | Rôles                                                                                     |
|------------|-------------------------------------------------------------------------------------------|
| .html      | La vue, gère l'affichage seulement.                                                       |
| .scss      | La feuille de style lié à la vue.                                                         |
| .ts        | Le contrôleur, fait le lien entre les fichiers du composant et avec le reste du logiciel. |
| .spec.ts   | Fichier de test unitaire.                                                                 |

**Note** : Angular va modifier toutes les balises de la vue et tous les sélecteurs CSS, il ajoute un attribut HTML, par exemple, '_ngcontent-gvp-c45'.

## Fonctionnement

Tout ce qui est publique dans la classe du contrôleur est disponible dans la vue (propriété et fonction). La classe est déjà formé de deux fonctions importante : 

- `constructor()` : le constructeur du component, appelé à la création de la composante.
- `ngOnInit()` : Cette fonction est appelé lorsque le gabarit (template) est généré et prêt à être manipulé. On va y inscrire le code à exécuter au démarrage du composant.

**Note** : Le constructeur va rester vide puisque en fait, tout ce que on pourrait faire dans le constructeur peut être fait dans `ngOnInit()` mais pas l'inverse et donc pour éviter de se tromper on va rarement toucher au constructeur.

## Afficher des variables

Pour afficher une valeur dans la vue, il faut la déclarer dans le contrôleur (la classe) puis utiliser les moustaches dans la vue pour afficher la valeur de la variable. <br>

Dans le fichier .ts :

```typescript
export class LoginComponent implements OnInit {

  count: number = 0; // Déclaration d'une variable (donnée membre)

  constructor() {}

  ngOnInit(): void {}
}
```

Et dans le fichier .html :

```html
<p>Compte: {{count}}</p>
```

## Fonctions de component

Pour utiliser une fonction, il faut lier une fonction du contrôleur à un événement DOM dans le HTML. Par exemple, on va ajouter un onClick sur un bouton qui incrémente le compte : <br>

Dans le fichier .ts :

```typescript
export class LoginComponent implements OnInit {

  count: number = 0;

  constructor() {}

  ngOnInit(): void {}

  inc() {
    this.count++;
  }
}
```

Et dans le fichier .html : 

```html
<p>Compte: {{count}}</p>

<button (click)="inc()">Compte++</button>
```

- Input/Output de component
- Services
- Injections de dépendance
- Gosser avec Import dans app.module
- Material
- Form Reactive

- Pluger Express.js