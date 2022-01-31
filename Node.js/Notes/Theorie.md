<style>
    .title{
        font-size: 37px;
        text-align: center;
        border-bottom: solid rgb(143, 143, 143);
        border-width:2px;
    }
</style>

<p class="title"> Théorie </p>

# Installation

## Windows

Pour la majorité des gens sur windows, l'installation est fort simple : 
1. Dirigez vous sur le site web de [Node.js](https://nodejs.org/en/).
2. Téléchargez l'installateur de la version qui vous convient.
3. Exécuter le fichier et suivre les étapes d'installations.

## Linux

Pour linux, l'installation de Node.js est quelque peu plus complexe. La version de Node.js dépend de votre "package manager", par exemple sur les ditributions basé sur arch, le paquet "nodejs" était à jour, cependant sur les ditributions basés sur Debian, la dernière version du paquet "nodejs" était la 10.
<br><br>
Cependant, si vous êtes sur Ubuntu, il est possible d'installer Node.js à l'aide du PPA officiel de Node.js et c'est cette façon que je vais montrer dans les étapes suivantes. Sinon, vous pouvez toujours vous repliez sur le [code source](https://nodejs.org/dist/v17.3.1/node-v17.3.1.tar.gz).

1. Ouvrez un terminal et rendez vous à votre dossier de téléchargement avec la commande suivante : `cd ~/Downloads/` ou encore `cd ~/Téléchargements/`
2. Téléchargez la version du script d'installation que vous voulez avec curl : `curl -sL https://deb.nodesource.com/setup_16.x -o nodesource_setup.sh`
3. Exécuter le script avec la commande suivante : `sudo -E bash nodesource_setup.sh`
4. Mettez à jour votre "package manager" avec : `sudo apt update -y && sudo apt upgrade -y`
5. Installez le paquet nodejs avec apt : `sudo apt install nodejs`
6. Vérifiez que Node.js est installé avec la bonne version : `node -v`

**Note** : À l'étape 2, vous pouvez changer 16.x pour 17.x ou un autre version si vous le souhaitez.

# Possibles erreurs à l'installation

Voici une mini-liste des erreures que vous pourriez rencontrez durant l'installation, si le lien est coché c'est que j'ai moi-même rencontrer le problème et la solution à fonctionnée.
<br>
[x] [dpkg: error processing archive unpack](https://github.com/nodesource/distributions/issues/1157)

# Qu'est-ce que Node.js

## Résumer

Node.js est un environnement de runtime qui sert à l'éxécution de code javascript sans navigateur web. En gros, Avant Node.js, du code javascript pouvait juste être exécuter dans un moteur javascript qui lui était dans un navigateur. Ceci apportait plusieurs problèmes. Premièrement, chaque navigateur avait leur moteur javascript qui eux avait tous leurs petites différences, ce qui faisait en sorte que le même code n'avait pas toujours le même résultat dépendant des moteurs. Deuxièmement, du code javascript ne pouvait qu'être éxécuter qu'à l'intérieur des navigateurs ce qui faisait de javascript un language peu flexible, qui servait à une poigné seulement de choses. En 2009, Ryan Dahl (inventeur de Node.js), à prit le moteur javascript de Chrome (V8, le plus rapide entre V8, Charka et SpiderMonkey) et en l'emballant dans un programme c++ nommé Node.exe! Donc, Node.js remplace l'environnement de runtime d'un navigateur et y met un environnement plus ouvert en terme de possibilités et de quantité d'objets (avec accès à l'OS, à la création se serveur HTTP, la gestion de fichiers sur disque et plus encore).