---
Titre: Installation d'un poste pour le développement sous Arch Linux
---

# Aperçu

Ceci est un guide d'installation d'un poste pour le développement sous Arch Linux. Il est réalisé dans le contexte de la SAE 1.01 de la 1ère année de BUT Informatique (2021-2022). Le sujet est disponible dans les documents.

# Dossier d'étude et de choix des solutions

## Pourquoi Arch Linux ?

Le système d'exploitation choisit est Arch Linux, c'est un OS de type Unix Libre issu de GNU/Linux. J'ai choisit d'installer Arch Linux car l'installation est bien plus détaillée et formatrice qu'un autre système (comme Ubuntu ou Debian) selon moi. Cela m'a permis de vraiment comprendre et connaître les étapes nécessaires à l'installation d'un OS. J'ai aussi été séduit par la philosophie de la distribution qui prône la liberté et l'implication dans son système. De plus, après avoir testé Arch Linux je l'ai trouvé bien plus stable et rapide que les autres OS que j'ai pu tester.

## Les outils que j'ai choisit

Nous avions pour mission de choisir différents outils permettant de répondre à des besoins, ils sont listés ci-dessous :

| Besoins                                                                            | Nombre d'outils différents demandés | Logiciels proposés |
| ---------------------------------------------------------------------------------- | :----------------------------------:| -------------------|
| Avoir des Gestionnaires de bureau/fenêtre (dont un qui vous plaise)                | 4                                   |                    |
| Compiler un programme C                                                            | 2                                   |                    |
| Regarder les pages de man de la libC                                               | 2                                   |                    |
| Lancer un `make`                                                                   | 1                                   |                    |
| Éditer du code source                                                              | 4                                   |                    |
| Déboguer du code                                                                   | 2                                   |                    |
| Naviguer sur le Web                                                                | 2                                   |                    |
| Naviguer sur le Web avec la version de firefox dans backports                      | 1                                   |                    |
| Éditer une image matricielle (png...)                                              | 2                                   |                    |
| Éditer une image vectorielle (svg)                                                 | 1                                   |                    |
| (Dé)Compresser les formats `targz` et `7z` et `rar`                                | 1                                   |                    |

Le poste devait aussi être configuré pour :
* Avoir deux utilisateurs: vous et "stagiaire"
* Pouvoir se connecter sur une autre machine avec `ssh`.
* Permettre à une autre machine de se connecter sur la vôtre.
* Installer un serveur web capable de lire vos pages perso (`userdir`).
* Écrire un service utilisateur qui se lance dès la connexion de l'utilisateur.
* Écrire un service qui se lance périodiquement.
* Installer un logiciel propriétaire en restreignant ses droits d'accès à votre environnement.

# Notice d'installation

## Prérequis

La machine sur laquelle j'ai réalisé l'installation est un ordinateur portable possédant un système Windows 11 et un sytème Linux Ubuntu.
Avant de commencer l'installation j'ai du créer une clé de boot pour qui servira à l'initier. Sur Windows j'ai téléchargé une image du système d'exploitation (fichier .iso) que j'ai trouvé sur le **[site français de Arch Linux](http://mir.archlinux.fr/iso/latest/)**, elle porte le nom "*archlinux-2021.12.01-x86_64.iso*". J'ai aussi téléchargé le logiciel Rufus et branché ma clé USB. Sur Rufus j'ai sélectionné le périphérique correspondant à ma clé USB, sélectionné l'image disque de Arch Linux et cliqué sur Démarrer. Une fois le statut affichant prêt, j'ai relancé mon ordinateur et suit tombé sur 

# Schéma d'architecture logicielle
