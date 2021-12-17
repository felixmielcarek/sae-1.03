---
Dossier: Etude et choix des solutions
---

# Dossier d'étude et de choix des solutions

## Choix du système d'exploitation

La première étape de la SAE était de choisir un OS de type Unix Libre. 

### GNU/Linux ou BSD

Le premier choix à faire était installer un OS de type GNU/Linux ou BSD. En me renseignant j'ai pris connaissance des différences et points communs qu'ils avaient. Cependant j'ai compris que pour l'utilisation à laquelle était destiné le système et pour le niveau que j'avais, choisir entre un de ses deux types d'OS ne changerait pas grand chose. Je me suis donc naturellement tourné vers un système GNU/Linux car je n'ai jamais utilisé de système BSD et je serais donc plus à l'aise et efficace sur ce que je connais (je prévois personnellement d'essayer FreeBSD par exemple dans le futur).

### Choisir sa distribution

Ma courte expérience (1 an et demi) sur des systèmes UNIX m'avait seulement permis de tester des distributions Debian et Ubuntu. Leur installation étant grandement accompagnée je n'ai pas été séduit par le fait d'en faire un guide se résumant à cliquer sur suivant. 

En me renseignant rapidement sur les différents autres systèmes d'exploitation, l'installation d'un système Arch Linux m'a paru très intéressante. En l'installant j'ai vraiment mieux compris comment fonctionnait un système (ce que j'adore dans l'informatique), et j'ai appris énormément de choses. 

Après avoir réussi à l'installer et l'avoir tester, j'ai aussi adoré l'utiliser pour plusieurs raisons qui rentrait parfaitement dans l'objectif de la SAE (à savoir un poste pour le dévellopement): d'abord par sa stabilité, je n'ai jamais eu aucun soucis avec mon système (autre que venant de moi, dans les configurations par exemple). Ensuite sa rapidité, que se soit dans l'execution de tâches (bien qu'elles ne soient pas forcément lourdes) ou juste au démarrage du sytème, j'ai vraiment senti la différence par rapport à Ubuntu. Et enfin la taille du système ma grandement séduit aussi, mon système Arch Linux était presque 5 fois mois lourd que mon Ubuntu.

J'ai donc choisit pour toutes ses raisons d'utiliser Arch Linux.

## Choix des solutions

### Les critères

Pour choisir les solutions, j'ai utilisé plusieurs critères dû au sujet. Dans tous les cas j'ai essayé de trouver des solutions libres et open-source car j'adhère aux principes qu'ils véhiculent. 

Comme le poste est destiné au développement il y avait aussi des contraintes d'efficacité, de rapidité, et de praticité.

Quand plusieurs choix était disponibles, j'ai aussi essayé de trouver des solutions plus confortables à utiliser quitte à perdre en performances. Le but d'avoir différentes solutions et aussi selon moi qu'elles répondent le plus différemment possible au même besoin pour pouvoir varier à volonté.

### Résumé des choix

| Besoin                                                                             | Nombre d'outils différents demandés | Logiciels proposés |
| ---------------------------------------------------------------------------------- | :----------------------------------:| -------------------|
| Avoir des Gestionnaires de bureau/fenêtre (dont un qui vous plaise)                | 4                                   |                    |
| Avoir deux utilisateurs: vous et "stagiaire"                                       |                                     |                    |
| Compiler un programme C                                                            | 2                                   |                    |
| Regarder les pages de man de la libC                                               | 2                                   |                    |
| Lancer un `make`                                                                   |                                     |                    |
| Éditer du code source                                                              | 4                                   |                    |
| Déboguer du code                                                                   | 2                                   |                    |
| Naviguer sur le Web                                                                | 2                                   |                    |
| Naviguer sur le Web avec la version de firefox dans backports                      | 1                                   |                    |
| Éditer une image matricielle (png...)                                              | 2                                   |                    |
| Éditer une image vectorielle (svg)                                                 | 1                                   |                    |
| (Dé)Compresser les formats `targz` et `7z` et `rar`                                | 1                                   |                    |

## Explications détaillées des choix

### Choix des gestionnaires de bureau/fenêtre



### Gestionnaire de paquets

* Installer un logiciel.
* Désinstaller un logiciel.
* Faire une recherche sur les paquets disponibles.
* Faire une mise à jour.
* Lister les fichiers installés par un paquet.
* Rechercher quel paquet contient un fichier donné.
  * Idem si le paquet n'est pas installé.

### Réseau

* Pouvoir se connecter sur une autre machine avec `ssh`.
* Permettre à une autre machine de se connecter sur la vôtre.
* Installer un serveur web capable de lire vos pages perso (`userdir`).

### Sauvegardes

* Faire une archive d'un répertoire (et de ses sous répertoires).
* Copier l'archive sur une clé USB.
* Copier l'archive via `scp` (vous pouvez vous entraîner sur `localhost`).

### Services (voir `systemd` ou autre selon OS)

* Savoir démarrer/stopper un service.
* Savoir en vérifier l'état.
* Savoir afficher les messages d'erreur.

### Divers

* Comment faire pour que le *stagiaire* n'ait pas accès aux données de votre compte ?

### Bonus

* Écrire un service utilisateur qui se lance dès la connexion de l'utilisateur.
* Écrire un service qui se lance périodiquement.
* Installer un logiciel propriétaire en restreignant ses droits d'accès à votre environnement.

