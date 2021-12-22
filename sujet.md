---
title: Installation d'un poste pour le développement
---

# Aperçu du sujet

En partant d'un besoin exprimé par un client, il faut identifier les outils les plus adaptés aux besoins, les installer, les configurer et
créer une notice d'installation et d'utilisation. 
Cette SAÉ permet d'expérimenter les missions d'installation de poste de travail.

Ce travail est fait en *monôme*. Vous aurez une quinzaine d'heures, mais ne vous laissez pas coincer par le temps (plus vous commencez tôt, plus vous aurez du temps pour résoudre vos problèmes).

**Note** : Ce sujet est susceptible d'évoluer au cours du semestre.

## Aperçu des livrables

- Dossier d'étude et de choix des solutions, 13 points. Cette partie sera aussi évaluée à l'oral.
- Notice d'installation et d'utilisation, 3 points. Cette partie sera aussi évaluée à l'oral.
- Présentation orale en anglais, 2 points. Il s'agit d'anglais technique. 
- Schéma de l'architecture logicielle, 2 points.

# Sujet détaillé

## Installation du système de base

Installez un OS de type *Unix libre* (Linux, BSD…). 

* Le système proposé sera adapté au développement et donnera un accès simple au réseau, permettant au moins la navigation Web.
* Votre installation pourra se faire sur machine virtuelle à l'IUT (VirtualBox) ou éventuellement sur un portable personnel (à discuter avec votre enseignant de système).
* Il s'agit d'un travail en monôme et en autonomie.

Vous devez installer et essayer sur votre système des outils répondant à des besoins (voir plus bas). Dans certains cas, nous vous demandons d'essayer plusieurs logiciels répondant au même besoin.

Le tableau ci-dessous vous donne une liste des besoins.

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

## Points indispensables à maîtriser

Cette liste n'est pas exhaustive.

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


# Détail des livrables

L'ensemble des documents seront écrits en `markdown`, rendus en `markdown` **et** en PDF (voir `pandoc` par exemple). Les schémas seront en [vectoriel](https://fr.wikipedia.org/wiki/Image_vectorielle).

## Dossier d'étude et de choix des solutions

Rédigez un dossier synthétique de trois pages maximum. 

Ce dossier reprend le tableau des besoins (voir plus haut) complété en indiquant par besoin les logiciels que vous proposez. 
Vous trierez la liste des logiciels proposés suivant vos préférences.


## Notice d'utilisation

La notice d'utilisation est ici à destination d'un utilisateur souhaitant reproduire à l'identique le système que vous avez créé.

Nous attendons à trouver dans votre notice d'utilisation l'application des compétences acquises en cours/TP de PPP sur la constitution et la réalisation d'un manuel utilisateur, ici "un guide d'installation".

Elle reprend les choix principaux que vous avez faits pendant l'installation. 

## Présentation orale

Lors de cette présentation orale de sept minutes (éventuellement échelonnée au cours des TP) vous présenterez à votre enseignant vos productions de la SAÉ (dossier d'étude et de choix des solutions, notice d'utilisation, schéma de l'architecture logicielle).

Votre enseignant évaluera le fond, la forme et votre capacité à répondre aux questions qu'il vous posera.

Cette présentation orale sera également l'occasion d'évaluer votre capacité à traduire à la volée en français, un texte technique en anglais (extrait d'une page de manuel, messages d'erreurs, ...), en rapport à vos cours/TP d'anglais sur la constitution d'un lexique. 

## Schéma d'architecture logicielle

Faites un schéma (donc en [vectoriel](https://fr.wikipedia.org/wiki/Image_vectorielle)) donnant les informations suivantes :
  
* Comment s'appelle l'élément logiciel qui gère votre carte réseau (comme un driver) ?
* Comment s'appelle l'élément logiciel qui gère votre carte graphique (comme un driver) ?
* Quel est le chemin du périphérique (*device*) qui représente votre carte graphique ?
* Quel est le nom du *serveur graphique* que vous utilisez ?
* Avec quel élément de votre schéma le gestionnaire de bureaux/fenêtres que vous utilisez communiquent ?

