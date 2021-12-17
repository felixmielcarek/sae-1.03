---
Dossier: Etude et choix des solutions
---

# Dossier d'étude et de choix des solutions

## Choix du système d'exploitation

La première étape de la SAE était de choisir un OS du type Unix Libre. 

### GNU/Linux ou BSD

Le premier choix à faire était installer un OS du type GNU/Linux ou BSD. En me renseignant j'ai pris connaissance des différences et points communs qu'ils avaient. Cependant j'ai compris que pour l'utilisation à laquelle était destiné le système et pour le niveau que j'avais, choisir entre un de ces deux types d'OS ne changerait pas grand-chose. Je me suis donc naturellement tourné vers un système GNU/Linux car je n'ai jamais utilisé de système BSD et je serais donc plus à l'aise et efficace sur ce que je connais (je prévois personnellement d'essayer FreeBSD par exemple dans le futur).

### Choisir sa distribution

Ma courte expérience (1 an et demi) sur des systèmes UNIX m'avait seulement permis de tester des distributions Debian et Ubuntu. Leur installation étant grandement accompagnée je n'ai pas été séduit par le fait d'en faire un guide se résumant à cliquer sur ```Suivant```. 

En me renseignant rapidement sur les différents autres systèmes d'exploitation, l'installation d'un système Arch Linux m'a paru très intéressante. En l'installant j'ai vraiment mieux compris comment fonctionnait un système (ce que j'adore dans l'informatique), et j'ai appris énormément de choses. 

Après avoir réussi à l'installer et l'avoir testé, j'ai aussi adoré l'utiliser pour plusieurs raisons qui rentraient parfaitement dans l'objectif de la SAE (à savoir un poste pour le développement): d'abord par sa stabilité, je n'ai jamais eu aucun souci avec mon système (autre que venant de moi, dans les configurations par exemple). Ensuite sa rapidité, que ce soit dans l'exécution de tâches (bien qu'elles ne soient pas forcément lourdes) ou juste au démarrage du système, j'ai vraiment senti la différence par rapport à Ubuntu. Et enfin la taille du système m'a grandement séduite aussi, mon système Arch Linux était presque 5 fois moins lourd que mon Ubuntu.

J'ai donc choisi pour toutes ses raisons d'utiliser Arch Linux.

## Choix des solutions

### Les critères

Pour choisir les solutions, j'ai utilisé plusieurs critères dus au sujet. Dans tous les cas j'ai essayé de trouver des solutions libres et open source car j'adhère aux principes qu'ils véhiculent. 

Comme le poste est destiné au développement il y avait aussi des contraintes d'efficacité, de rapidité, et de praticité.

Quand plusieurs choix étaient disponibles, j'ai aussi essayé de trouver des solutions plus confortables à utiliser quitte à perdre en performances. Le but d'avoir différentes solutions et aussi selon moi qu'elles répondent le plus différemment possible au même besoin pour pouvoir varier à volonté.

### Résumé des choix

| Besoin                                                                             | Nombre d'outils | Logiciels proposés                 |
| ---------------------------------------------------------------------------------- | :--------------:| :---------------------------------:|
| Avoir des Gestionnaires de bureau/fenêtre (dont un qui vous plaise)                | 4               | xfce - i3 - gnome - xorg-twm       |
| Compiler un programme C                                                            | 2               | gcc - clang                        |
| Regarder les pages de man de la libC                                               | 2               | man-db - glibc                     |
| Lancer un `make`                                                                   |                 | base-devel                         |
| Éditer du code source                                                              | 4               | vim - VScode - geany - Rider       |
| Déboguer du code                                                                   | 2               | gdb - LLDB                         |
| Naviguer sur le Web                                                                | 2               | Firefox - Opera                    |
| Éditer une image matricielle (png...)                                              | 2               | Gimp - Krita                       |
| Éditer une image vectorielle (svg)                                                 | 1               | Inkscape                           |
| (Dé)Compresser les formats `targz` et `7z` et `rar`                                | 1               | gzip                               |

## Explications détaillées des choix

### Choix des gestionnaires de bureau/fenêtre

J'ai d'abord choisi xfce comme premier gestionnaire de bureau/fenêtre car s'est-il est très moyen/basique partout, il satisfait donc en théorie le plus grand nombre. De plus Linus Torvalds lui-même a conseillé d'utiliser xfce lors de la sortie de Gnome 3 (je suis facilement influençable).

En deuxième choix j'ai choisi i3 (i3-gaps pour être précis) car c'est le gestionnaire de fenêtres que je préfère par-dessus tout, il est très rapide et configurable à souhait, il faut juste un petit peu de pratique pour l'utiliser efficacement dû aux raccourcis claviers inhabituels. J'ai préféré i3-gaps à i3-wm car je trouve que l'espacement des fenêtres est très joli et rend l'écran plus lisible à mon goût.

Mon troisième choix a porté sur gnome, je n'apprécie pas du tout ce gestionnaire à cause de sa lenteur et sa lourdeur due aux nombreux paquets qu'il installe par défaut. Cependant je dois reconnaître à gnome qu'il est confortable visuellement et qu'il est apprécié par de nombreux utilisateurs, c'est ce qui a motivé mon choix.

Finalement mon dernier choix est celui de xorg-twm, j'ai installé ce gestionnaire pour tester l'opérabilité de mon serveur d'affichage X (avec la commande startx). Bien qu'il soit horrible inutilisable au quotidien (selon moi), ça reste un gestionnaire de fenêtres fonctionnel et très pratique lors de l'installation.

### Choix des compilateurs C

Le premier compilateur C que j'ai choisi est logiquement gcc. Logiquement car le noyau Linux dépend étroitement des fonctionnalités de gcc, c'est aussi le compilateur avec lequel je suis le plus à l'aise puisque je l'utilise depuis plus d'un an.

Une alternative à gcc que je ne connaissais pas est Clang. De mes recherches j'ai compris que sa manière de compiler du code est différente de gcc et à pour objectif de garder un maximum les informations du code original (contrairement à gcc). Cela permet d'avoir des rapports d'erreurs plus détaillés ce qui facilite la traçabilité d'un problème. Pour ces raisons, cette solution semble intéressante pour certains projets de développement.

### Regarder les pages de man de la libC

Le premier outil est man-db qui permet d'utiliser la commande man 3 suivit du manuel que l'on souhaite consulter. Cet outil est très pratique pour consulter des pages de manuel directement dans son terminal. L'option 3 est pour les manuels concernant le langage C. Le désavantage à cet outil est la traduction des pages qui est parfois maladroite.

Le deuxième outil est glibc. C'est une library qui contient les fonctionnalités du système GNU/Linux. Il est bien moins pratique à consulter puisque je n'ai pas trouvé de commande pour consulter les manuels, cependant une recherche internet nous procure rapidement une solution.

### Lancer un `make`

La commande make est disponible dans le paquet base-devel.

### Editer du code source

Mon premier choix porte sur vim. Bien que certaines personnes le critique pour sa prise en main rebutante, je trouve que cet outil est avec un peu de pratique très performant et procure un gain de temps incroyable. Il est très rapide dans son fonctionnement, très léger et avec quelques plugins bien choisis, n'a rien à envier aux IDE les plus populaires.

Mon deuxième choix est Visual Studio Code, cette IDE est plus joli que vim et possède beaucoup de fonctionnalités intégrées ou faciles à intégrer. Cela ajoute forcément du poids au logiciel cependant.

Geany est un IDE que je n'ai presque jamais utilisée mais que je trouve très pratique. Il est assez basique, l'interface est claire est fonctionnelle même si je ne la trouve pas très jolie.

Enfin, le dernier outil que j'ai choisi est Rider. Bien que je ne l'ai pas encore testé cet IDE semble particulièrement efficace pour développer en C#, contrairement à Visual Studio que je trouve horriblement lent.

### Déboguer du code

Pour choisir deux débogueurs, j'ai tout simplement choisi ceux correspondant aux projets possédants les compilateurs que j'avais installés. Pour le projet GNU c'est donc gdb qui correspond et pour LLVM c'est LLDB.

### Naviguer sur le Web

Le premier navigateur internet que j'ai installé est Firefox, je le trouve très pratique à utiliser et possède toutes les fonctionnalités qu'on attend de lui. De plus Firefox a (plus ou moins) une éthique de protection des données ce qui n'est pas négligeable.

Le deuxième navigateur que j'ai choisi est Opera. J'ai longtemps utilisé Opera par le passé pour ses nombreuses petites fonctionnalités intérressantes, notemment dans l'intégration d'applications. J'ai cessé de l'utiliser pour sa lourdeur et sa lenteur mais je sais qu'il séduit un grand nombre de personnes.

### Editer une image matricielle

Gimp est assurément la meilleure alternative libre aux licences payantes (comme Adobe), son interface c'est grandement amélioré et de nombreuses fonctionnalités intéressantes sont disponibles (comme la possibilité d'exporter une image comme du code C par exemple).

Krita est un logiciel très utile et fonctionnel pour les dessinateurs spécialement, notamment grâce à une bonne intégration de l'usage de la tablette graphique. Des connaissances à moi travaillant dans le domaine de l'art utilisent et apprécient cet outil.

### Editer une image vectorielle

Je ne connaissais pas l'existence des images vectorielles avant le début de cette SAE et me suis donc renseigné sur son fonctionnement basique et sur les logiciels permettant d'en éditer. Adobe Illustrator semble être le meilleur logiciel dans le domaine mais est sous licence payante, cependant Inkscape présente (presque) les mêmes fonctionnalités et est libre. J'ai donc essayé ce logiciel pour réaliser le schéma de l'architecture logicielle et ai remarqué qu'il remplissait effectivement parfaitement son rôle. Dû au fait que je ne l'ai utilisé qu'une fois, je n'ai pas trouvé la prise en main très facile et l'interface n'était pas très belle selon moi cependant.

### (Dé)Compresser les formats targz et 7z et rar

gzip est l'outil fourni par le projet GNU, il est suffisamment simple d'utilisation en ligne de commande. Je n'ai pas voulu installer de logiciel graphique car je considère qu'ils sont une perte de temps considérable pour ce genre de petites manipulations. Le confort gagné n'aurait été que minime selon moi.

## Points indispensables à maîtriser

### Gestionnaire de paquets

#### Installer un logiciel

```
sudo pacman -S nom_du_paquet
```

#### Désinstaller un logiciel

```
sudo pacman -Rsn nom_du_paquet
```

#### Faire une recherche sur les paquets disponibles

Recherche d'un paquet parmi ceux installés:

```
pacman -Qs nom_du_paquet
```

Recherche d'un paquet dans les dépôts:

```
pacman -Ss nom_du_paquet
```

#### Faire une mise à jour

```
sudo pacman -Syu
```

#### Lister les fichiers installés par un paquet

```
pacman -Ql paquet_1
```

#### Rechercher quel paquet contient un fichier donné

```
pacman -Qo /chemin/vers/le/fichier
```

### Réseau

#### Permettre à une autre machine de se connecter sur la vôtre

```
pacman -S openssh
```

```
vim /etc/ssh/sshd_config
```

Décommenter la ligne sur le port.

```
ip addr
```

Trouver adresse MAC.

```
systemctl enable sshd
systemctl start sshd
```

Il faut maintenant configurer mon routeur, interface Freebox OS dans un navigateur > Paramètres de la Freebox > DHCP > Baux statiques > Ajouter un bail DHCP statique > Adresse MAC: adresse MAC de Arch > Adresse IP: choisir une adresse > Sauvegarder.

Paramètres de la Freebox > Gestion des ports > Ajouter une redirection > IP Destination: IP choisi avant > IP source: Toutes > Port de début: choisir au-dessus de ce qui est indiqué > Port de destination: 22 > Sauvegarder.

Création des clefs sur la machine client et ajout dans .ssh/ de la machine serveur.

```
ssh felix@adresse.ip.publique.freebox -p PORT_CHOISIT
```

#### Pouvoir se connecter sur une autre machine avec `ssh`

Création des clefs sur la machine client et ajout dans .ssh/ de la machine serveur.

```
ssh login@adresse.ip
```

#### Installer un serveur web capable de lire vos pages perso (`userdir`)

```
pacman -S apache
```

```
systemctl enable httpd
systemctl start httpd
```

```
vim /srv/http/index.html
```

Créer page html et vérifier avec localhost dans un navigateur.

### Sauvegardes

#### Faire une archive d'un répertoire (et de ses sous répertoires)

```
tar -cvf nom_archive.tar nom_dossier/
gzip nom_archive.tar
```

#### Copier l'archive sur une clé USB

```
mount /dev/nom_partition_clef /mnt
cp /chemin/de/l/archive /mnt
umount /dev/nom_partition_clef
```

#### Copier l'archive via `scp`

Connexion ssh fonctionnelle requise.

```
scp /chemin/de/l/archive login@adresse.ip:/repertoire/destination
```

### Services

#### Savoir démarrer/stopper un service

```
systemctl start service
systemctl stop service
```

#### Savoir en vérifier l'état

```
systemctl status service
```

#### Savoir afficher les messages d'erreur

Les messages d'erreurs sont dans les fichiers de logs dans le répertoire /var/log/.

### Divers

#### Comment faire pour que le *stagiaire* n'ait pas accès aux données de votre compte ?

```
chmod 700 /home/felix
```
