---
Titre: Installation d'un poste pour le développement sous Arch Linux
---

# Aperçu

Ceci est un guide d'installation d'un poste pour le développement sous Arch Linux. Il est réalisé dans le contexte de la SAE 1.01 de la 1ère année de BUT Informatique (2021-2022). Le sujet est disponible dans les documents.

# Dossier d'étude et de choix des solutions

## Pourquoi Arch Linux ?

Le système d'exploitation choisit est Arch Linux, c'est un OS de type Unix Libre issu de GNU/Linux. J'ai choisit d'installer Arch Linux car l'installation est bien plus détaillée et formatrice qu'un autre système (comme Ubuntu ou Debian) selon moi. Cela m'a permis de vraiment comprendre et connaître les étapes nécessaires à l'installation d'un OS. J'ai aussi été séduit par la philosophie de la distribution qui prône la liberté et l'implication dans son système. De plus, après avoir testé Arch Linux je l'ai trouvé bien plus stable et rapide que les autres OS que j'ai pu tester.

## Les outils que j'ai choisit

# Notice d'installation

## Prérequis

La machine sur laquelle j'ai réalisé l'installation est un ordinateur portable possédant un système Windows 11 et un sytème Linux Ubuntu, le disque n'est pas plein puisque qu'il reste de l'espace qui n'est pas utilisé.
Avant de commencer l'installation j'ai du créer une clé de boot qui servira à l'initier. Sur Windows j'ai téléchargé une image du système d'exploitation (fichier .iso) que j'ai trouvé sur le **[site français de Arch Linux](http://mir.archlinux.fr/iso/latest/)**, elle porte le nom "*archlinux-2021.12.01-x86_64.iso*". J'ai aussi téléchargé le logiciel Rufus et branché ma clé USB. Sur Rufus j'ai sélectionné le périphérique correspondant à ma clé USB, sélectionné l'image disque de Arch Linux et cliqué sur Démarrer, Rufus formate entièrement ma clé et place les fichiers du fichier .iso dessus. Quand le statut de Rufus affiche prêt c'est que la clé est fini d'être configuré et peut permettre de faire l'installation.
Une fois le statut affichant prêt, j'ai relancé mon ordinateur et suis tombé directement sur le menu d'installation de Arch Linux. En effet dans mon UEFI j'avais lors de mon installation Ubuntu en dual boot déjà désactivé le Secure Boot et le Fast Boot, j'avais aussi mis en premier périphérique à boot mon entrée USB et en deuxième périphérique mon grub installé sur mon disque dur (qui se lance par défaut quand il n'y a pas de clé de boot inséré).

## Installation du système d'exploitation

Dans le menu d'installation de Arch Linux, je sélectionne l'option ```Arch Linux install medium (x86_64, UEFI)```.

Ensuite j'obtiens un terminal *archiso* où je suis connecté en *root*. La première chose que je fais pour me faciliter toutes les commandes est le changement de mes touches de QWERTY à AZERTY, pour cela j'entre la commande ```loadkeys fr```.

La première chose à faire est d'activer internet, mon ordinateur portable n'a pas de prise ethernet, je dois donc utiliser l'utilistaire iwd pour configurer ma connexion wifi. Je lance la commande iwctl pour obtenir un affichage intéractif. Je lance la commande device list pour obtenir la liste des cartes réseaux wifi de ma machine. Dans mon cas c'est wlan0. Ensuite je demande à ma carte wifi de scanner les différentes connexions puis de les afficher:

```
station wlan0 scan
```

```
station wlan0 get-networks
```

Je vois dans les connections wifi affichées ma box: Freebox-89E501. Je me connecte avec la commande station wlan0 connect Freebox-89E501. Après avoir appuyer sur Entrée on me demande le mot de passe de ma box que j'entre.

Pour tester ma connexion je sors de mon interface iwd avec exit et j'entre la commande *ping 8.8.8.8*. Si la commande me renvoie une réponse c'est que je peux atteindre le serveur DNS de Google (celui correspondant à l'adresse 8.8.8.8) et suis donc connecté à internet.

Pour vérifier que l'horloge de notre système est précise je commence par activer la synchronisation avec les serveurs de temps grâce à la commande timedatectl set-ntp true.
En tapant la commande timedatectl status je peux voir que mon horloge est maintenant synchronisé. En revanche le fuseau horaire n'est pas forcément bon. Dans mon cas mon sytème possède 1h de retard, pour ajuster cela je configure mon fuseau horaire avec la commande timedatectl set-timezone Europe/Paris. Je peux vérifier que tout c'est bien déroulé en affichant le status de timedatectl comme précédemment.

Maintenant il faut partitionner mon disque dur. La commande fdisk -l me permet d'afficher des informations sur mes disques. Je retrouve le disque dur de mon ordinateur qui est divisé en 7 partitions dans mon cas. Je retrouve aussi ma clé USB (composé logiquement d'une seule partition) mais ce n'est pas ce qui m'intéresse.
Mon disque dur est /dev/nvme0n1, j'effectue donc la commande cfdisk /dev/nvme0n1 pour commencer à le manipuler. La commande me liste mes partitions ainsi que mon espace libre Free space en vert, j'utilise les flèches du claviers pour selectionner cette emplacement puis en bas je positionne la selection sur New et j'appuis sur Entrée.
Je vais créer ma partition principale, pour la **Partition size:** j'écris 50G pour donner une taille de 50 Go, je n'ai pas à changer son type car par défaut une partition créé est de type Linux filesystem (ce qu'on veut). Je n'ai pas non plus de partition EFI à créer car elle existe déjà comme j'ai plusieurs système déjà installé. J'ai choisi de ne pas faire de partition Swap non plus car ma RAM est suffisement grande à mon goût. Pour valider ce que je viens de faire et écrire directement sur le disque mes modifications je sélectionne Write et écrit yes pour revalider. Je peux finalement sélectionner Quit pour revenir dans mon terminal.
Je peux refaire un fdisk -l pour vérifier que tout est bon, j'en profite pour regarder le nom de ma nouvelle partition: /dev/nvme0n1p8.
Maintenant que ma partition est créée il faut la formater, pour cela j'utilise la commande mkfs.ext4 /dev/nvme0n1p8 qui formate la partition au format ext4 qui est le plus utilisé sous Linux. Je vérifie que toute les étapes affichent le message done.

Ensuite il faut monter la partition pour pouvoir continuer la configuration de mon système, pour cela j'utilise la commande mount /dev/nvme0n1p8 /mnt. Cette étape permet d'accéder à mon futur système depuis une "session live" temporaire qui est présente sur ma clé de boot (c'est le repertoire /mnt).

Maintenant je dois installer l'architecture principal de mon système Arch Linux (je passe donc maintenant et pour les prochaines commandes par /mnt pour modifier directement mon futur système), pour cela j'utilise la commande pacstrap /mnt base linux linux-firmware vim networkmanager sudo grub xorg.
Pacstrap installe:
* base qui est le sytème de base de arch
* linux qui est le noyau linux (kernel)
* linux-firware qui est un paquet permettant au kernel de fonctionner
Dans les paquets installés par pacstrap se trouve le programme pacman qui permet d'installer d'autres paquets sur Arch Linux. C'est donc pacman qui prend la main automatiquement pour installer les paquets que j'installe en prévision, c'est à dire:
* vim qui me permettra de modifier mes fichiers
* networkmanager qui me permettra de me connecter à internet
* sudo qui me permettra d'utiliser les commandes en tant qu'administrateur
* grub qui me permettra de configurer mon grub déjà installer pour qu'il reconnaisse mon nouveau système
* xorg qui me permettra d'utiliser un interface graphique

# Schéma d'architecture logicielle
