---
Notice: Installation - Utilisation
---

# Notice d'installation

## Prérequis

### Le matériel disponible

La machine sur laquelle j'ai réalisé l'installation est un ordinateur portable possédant un système ```Windows 11``` et un sytème ```Linux Ubuntu```, le disque n'est pas plein puisque qu'il reste de l'espace qui n'est pas utilisé.

### Création d'une clé de boot

Avant de commencer l'installation j'ai du créer une clé de boot qui servira à l'initier.

Sur Windows j'ai téléchargé une image du système d'exploitation (fichier ```.iso```) que j'ai trouvé sur le **[site français de Arch Linux](http://mir.archlinux.fr/iso/latest/)**, elle porte le nom ```archlinux-2021.12.01-x86_64.iso```.

J'ai aussi téléchargé le logiciel ```Rufus``` et branché ma clé USB.

Sur Rufus j'ai sélectionné le périphérique correspondant à ma clé USB, sélectionné l'image disque de Arch Linux et cliqué sur ```Démarrer```, Rufus formate entièrement ma clé et place les fichiers du fichier ```.iso``` dessus.

Quand le statut de Rufus affiche ```prêt``` c'est que la clé est fini d'être configuré et peut permettre de faire l'installation.

Une fois le statut affichant prêt, j'ai relancé mon ordinateur et suis tombé directement sur le menu d'installation de Arch Linux.

En effet dans mon ```UEFI``` j'avais lors de mon installation Ubuntu en dual boot déjà désactivé le ```Secure Boot``` et le ```Fast Boot```, j'avais aussi mis en premier périphérique à boot mon entrée USB et en deuxième périphérique mon grub installé sur mon disque dur (qui se lance par défaut quand il n'y a pas de clé de boot inséré).

## Installation du système d'exploitation


!!!!!!!!!!!!!!!!!!!DETAILLER TOUT LES -options !!!!!!!!!!!!!!!!!!!


Dans le menu d'installation de Arch Linux, je sélectionne l'option ```Arch Linux install medium (x86_64, UEFI)```. Ensuite j'obtiens un terminal ```archiso``` où je suis connecté en ```root```. 

### Changer ses touches en layout AZERTY

```
loadkeys fr
```

### Activer internet

La première chose à faire est d'activer internet, mon ordinateur portable n'a pas de prise ethernet, je dois donc utiliser l'utilistaire ```iwd``` pour configurer ma connexion wifi. 

#### Affichage intéractif ```iwd```

```
iwctl
```

#### Lister les cartes réseaux wifi

```
device list
```

Dans mon cas c'est ```wlan0```. 

#### Scanner les connexions disponibles

```
station wlan0 scan
```

#### Afficher les connexions scannées

```
station wlan0 get-networks
```

Je vois dans les connections wifi affichées ma box: ```Freebox-89E501```. 

#### Se connecter à un réseau wifi

```
station wlan0 connect Freebox-89E501
```

Après avoir appuyer sur Entrée on me demande le mot de passe de ma box que j'entre. Pour sortir j'entre:

```
exit
```

#### Tester sa connexion

```
ping 8.8.8.8
```

Si la commande me renvoie une réponse c'est que je peux atteindre le serveur DNS de Google (celui correspondant à l'adresse ```8.8.8.8```) et suis donc connecté à internet.

### Configurer l'horloge de son système

#### Vérifier précision de l'horloge

J'activer la synchronisation avec les "serveurs de temps" grâce à la commande:

```
timedatectl set-ntp true
```

#### Consulter l'état de mon horloge

```
timedatectl status
```

Je peux voir que mon horloge est maintenant synchronisé. 

#### Changer fuseau horaire

Dans mon cas mon sytème possède 1h de retard, pour ajuster cela je configure mon fuseau horaire avec la commande:

```
timedatectl set-timezone Europe/Paris
```

### Partitionner le disque dur

#### Afficher des informations sur les disques

```
fdisk -l
```

Je retrouve le disque dur de mon ordinateur qui est divisé en 7 partitions dans mon cas. Je retrouve aussi ma clé USB (composé logiquement d'une seule partition) mais ce n'est pas ce qui m'intéresse.

#### Manipuler un disque

Mon disque dur est ```/dev/nvme0n1```, j'effectue donc la commande:

```
cfdisk /dev/nvme0n1
``` 

La commande me liste mes partitions ainsi que mon espace libre ```Free space``` en vert.

#### Création des partitions

J'utilise les flèches du claviers pour selectionner l'emplacement libre puis en bas je positionne la selection sur ```New``` et j'appuis sur Entrée.

Je vais créer ma partition principale, pour la ```Partition size:``` j'écris 50G pour donner une taille de 50 Go, je n'ai pas à changer son type car par défaut une partition créé est de type Linux filesystem (ce qu'on veut).

Je n'ai pas non plus de partition EFI à créer car elle existe déjà comme j'ai plusieurs système déjà installé.

J'ai choisi de ne pas faire de partition Swap non plus car la capacité de ma RAM est suffisement grande à mon goût. 

Pour valider ce que je viens de faire et écrire directement sur le disque mes modifications je sélectionne ```Write``` et écrit ```yes``` pour revalider.

Je peux finalement sélectionner ```Quit``` pour revenir dans mon terminal.

Je peux refaire un fdisk -l pour vérifier que tout est bon, j'en profite pour regarder le nom de ma nouvelle partition: /dev/nvme0n1p8.

#### Formater la partition

```
mkfs.ext4 /dev/nvme0n1p8
```

Cette commande formate la partition au format ```ext4``` qui est le plus utilisé sous Linux. Je vérifie que toute les étapes affichent le message ```done```.

### Configuration du système

#### Monter la partition

```
mount /dev/nvme0n1p8 /mnt
```

Cette étape permet d'accéder à mon futur système depuis une "session live" temporaire qui est présente sur ma clé de boot (c'est le repertoire ```/mnt```). Je passe donc maintenant et pour les prochaines commandes par ```/mnt``` pour modifier directement mon futur système).

#### Installer architecture principale

```
pacstrap /mnt base linux linux-firmware vim networkmanager sudo grub xorg
```

```Pacstrap``` installe:
* ```base``` qui est le sytème de base de Arch Linux
* ```linux``` qui est le noyau linux (```kernel```)
* ```linux-firware``` qui est un paquet permettant au ```kernel``` de fonctionner

Dans les paquets installés par ```pacstrap``` se trouve le programme ```pacman``` qui permet d'installer d'autres paquets sur Arch Linux. C'est donc pacman qui prend la main automatiquement pour installer les paquets que j'installe en prévision, c'est à dire:
* ```vim``` qui me permettra d'éditer mes fichiers
* ```networkmanager``` qui me permettra de me connecter à internet
* ```sudo``` qui me permettra d'utiliser les commandes en tant qu'administrateur
* ```grub``` qui me permettra d'avoir un grub pour lancer mes systèmes au démarrage de la machine
* ```xorg``` qui me permettra d'utiliser un interface graphique

#### Editer la configuaration de montage des systèmes de ma machine

```
genfstab -U /mnt >> /mnt/etc/fstab
```

Le fichier fstab contient les configurations de montage des systèmes de ma machine.

#### Se chrooter

```
arch-chroot /mnt
```

Cela me permet d'entrer dans un environnement isolé, ce qui signifie que je ne peut pas accéder aux fichiers et aux commandes du système hôte. Cela reviens à être connecter en tant que root sur notre système.

#### Configurer le fuseau horaire

```
ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime
```

#### Configurer l'horloge du système

```
hwclock --systohc
```

#### Editer les paramètres régionaux

Le fichier locale.gen contient les paramètres régionaux. Je tape la commande

```
vim /etc/locale.gen
```

Une fois dans le fichier je recherche la ligne que je veux en tapant:

```
/fr_FR.UTF-8
```

Je tape ```Entrée``` et je décommente la ligne sur laquelle je me trouve. 

Pour générer les paramètres du fichier que je viens d'éditer:

```
locale-gen
```

#### Donner un nom au système

```
vim /etc/hostname
```

J'écris ensuite dans le fichier le nom choisit: ```fm-arch-sae``` dans mon cas.

#### Créer le fichier de hosts

```
vim /etc/hosts
```

Dans ce fichier il faut écrire les lignes suivantes:

```
127.0.0.1   localhost
::1         localhost
127.0.1.1   fm-arch-sae
```

Ce fichier permet au système d'associer des noms d'hôtes à des adresses IP lors de l'accès à un réseau. !!!!!!!!!!!!!!!!!!!!!!!!!!!!!

### Configurer les utilisateurs

#### Donner mot de passe à root

```
passwd
``` 

J'entre mon mot de passe (puis le confirme).

#### Créer d'utilisateurs

Je vais maintenant créer mes utilisateurs normaux, d'abord ```felix```, je tape la commande:

```
useradd -m felix
```

Je lui attribue un mot de passe avec la commande:

```
passwd felix
```

Je répète ces 2 opérations pour créer ```stagiaire```.

#### Attribuer des groupes aux utilisateurs

Je vais maintenant attribuer des groupes à mes utilisateurs pour qu'ils aient accès à certaines fonctions, pour ```felix``` je tape la commande:

```
usermod -aG wheel,audio,video,optical,storage,lp felix
```

Et pour stagiaire la même commande sans le ```wheel``` (je ne veux pas qu'il ait accès au commandes ```sudo```).

Les groupes précédents correspondent à:
* ```wheel```: ce groupe est utilisé pour donner à l'utilisateur l'accès à ```sudo``` sur certaines commandes et donc de droits administrateurs
* ```audio```: accès au matériel son
* ```video```: accès aux périphériques de capture vidéo
* ```optical```: accès au lecteur optique (cd/dvd)
* ```storage```: accès aux périphériques amovibles (ex: clé/disque usb)
* ```lp```: accès à l'imprimante

#### Modifier les droits ```sudo```

Il faut maintenant modifier le fichier /etc/sudoers qui contient des informations sur la commande sudo. Pour entrer directement dans le fichier j'entre la commande:

```
visudo
```

Il faut maintenant décommenter la ligne ```%wheel ALL=(ALL) ALL``` (recherchez avec ```/```), les utilisateurs dans le groupe ```wheels``` peuvent maintenant utiliser toutes les commandes en renseignant ```sudo``` et en entrant le mot de passe.

### Préparer le ```boot```

#### Installer les paquets essentiels

Entrer la commande:

```
pacman -S efibootmgr dosfstools os-prober mtools
```

J'ai installé les paquets suivants !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!:
* ```efibootmgr```
* ```dosfstools```
* ```os-prober```
* ```mtools```

#### Création du répertoire de boot

```
mkdir /boot/EFI
```

#### Monter la partition de boot

Je monte ma partition ```EFI System``` déjà existante (c'est ```/dev/nvme0n1p2``` dans mon cas) dans le répertoire tout juste créé avec:

```
mount /dev/nvme0n1p2 /boot/EFI
```

### Préparer le ```grub```

#### Installer ```grub```

```
grub-install --target=x86_64-efi --bootloader-id=grub_arch_sae --recheck
```

Si tout se déroule bien un message avec ```No error reported``` apparait.

#### Généner la configuration du grub

```
grub-mkconfig -o /boot/grub/grub.cfg
```

### Préparer le démarrage

#### Activer ```NetworkManager```

```
systemctl enable NetworkManager
```

#### Sortir de ```arch-chroot```

```
exit
```

#### Démonter la "partition live"

```
umount -l /mnt
```

#### Eteindre mon ordinateur

```
shutdown now
```

### Démarrer Arch Linux

J'enlève ma clé USB et ensuite je rallume la machine.

Ma machine se lance et affiche le ```grub``` déjà présent sans l'option de boot sur le système Arch Linux que je viens d'installer, en effet le programme ```os-prober``` ne sait pas qu'il doit aller chercher ma partition est la donner au ```grub``` actuel. 

#### Activer la partition

Pour cela il faut faire deux choses, après m'être connecté sur ma partition qui lance le ```grub```, j'ajouter dans le fichier ```/boot/default/grub``` la ligne ```GRUB_DISABLE_OS_PROBER=false``` pour que le ```os-prober``` aille chercher les autres systèmes (j'ai déjà réalisé cette étape lors de mes précédentes installations). 

Ensuite il faut que j'actualise la configuration du grub avec:

```
sudo grub-mkconfig -o /boot/brub/grub.cfg
```

En relançant mon ordinateur maintenant (```reboot```), j'obtiens le même ```grub``` mais avec l'option Arch Linux sur la partition ```/dev/nvme0n1p8```, je la selectionne et peut me connecter sur mon compte utilisateur créé précédemment.

### Configurer la session

#### Changer le langage du clavier

Je dois de nouveau changer le langage de mon clavier avec sudo cette fois. 

Pour avoir un clavier AZERTY dès le lancement de ma machine je tape la commande suivante:

```
echo KEYMAP=fr > /etc/vconsole.conf
```

Cela créé un fichier de configuration du sytème qui sera lu par ```systemd``` dès le lancement.

#### Se connecter à internet

##### Lister réseaux wifi disponibles

```
nmcli device wifi list
```

##### Se connecter à un réseau

```
nmcli device wifi connect Freebox-89E501 password
```

J'ajoute le mot de passe de ma box. 

##### Vérifier sa connexion

```
ping google.com 
```

### Tester le serveur graphique

Je vais maintenant tester que mon serveur graphique ```xorg``` fonctionne correctement, je vais donc lancer l'environnement minimaliste. 

Pour cela je dois installer des paquets à l'aide de la commande suivante:

```
pacman -S xorg-xinit xorg-twm xorg-xclock xterm
```

Je peux ensuite lancer la commande ```startx``` qui me lance l'interface graphique. En entrant ```exit``` dans le terminal à haut à gauche je peux quitter ```startx```.

### Installer le gestionnaire d'affichage

```
sudo pacman -S lightdm lightdm-gtk-greeter
```

Le deuxième paquet est un interface utilisateur qui est nécessaire. 

### Activer le serveur graphique

```
systemctl enable lightdm.service
```

### Installer l'environnement de bureau

J'installe le groupe de paquet ```xfce4```, je dois appuyer une deuxième fois sur ```Entrée``` pour installer tous les paquets du groupe, puis je ```reboot```. 

J'arrive sur ```lightdm```, je me connecte et arrive sur ```xfce```.

### Changer langue du clavier

Il faut que je rechange mon clavier en AZERTY, pour cela ```Applications``` (en haut à gauche) > ```Settings``` > ```Keyboard``` > ```Layout```, je décoche ```Use system defaults```, selectionne ```English``` et clique sur ```Edit``` puis selectionne le layout de clavier ```French```.

### Installer un navigateur web

Je lance un terminal (Ctrl+Alt+T) et j'installe le paquet ```firefox```, selectionne le thème de ```font``` que je veux (1 dans mon cas).

**Mon système est maintenant opérationnel et permet une navigation web basique.**
