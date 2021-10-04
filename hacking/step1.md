## Gestion des mises à jour
Bien souvent, il convient de faire une mise à jour du dépôt APT pour obtenir la liste des derniers paquets à installer.

En français, cela signifie qu'il y a par exemple une application **MonLogiciel** qui est passée en version **2**. On demande donc au système de nous chercher les informations sur les versions de ces logiciels mis à jour. 

Pour ce faire, on tape la commande suivante :
`apt-get update`

**Note 1:** la commande apt est propre aux distributions Linux Debian et dérivés. C'est-à-dire Ubuntu, Kali Linux, etc... mais d'autres distributions peuvent utiliser une autre commande pour cela ! **On ne va pas l'utiliser pour cet exemple**.

**Note 2:** bien souvent, on tapera "`sudo`" avant de taper cette commande. `Sudo` permet de dire "exécute cette commande **en tant qu'administrateur**". Pourquoi ? parce qu'il peut y avoir **plusieurs utilisateurs sur un même système** et tout le monde n'a pas le droit de tout changer, sinon il risque d'y avoir des soucis. Imaginez comme si c'était à l'école, avec les élèves possédant chacun leur compte, et l'enseignant ayant aussi le sien. Seul l'enseignant à les droits d'administrateur pour modifier des choses importantes. Ce compte administrateur s'appelle aussi "root" sous Linux !


Si l'on vous dit que vous n'êtes pas "root", c'est que vous n'êtes pas administrateur...

Vous avez de ce fait vu le système chercher des mises à jour de paquets.
Parfait ! Continuons.

Maintenenant, et si besoin, nous pouvons mettre à jour concrètement un logiciel (ou plusieurs) grâce à la dernière version en notre connaisssance.

On peut d'abord observer la liste des logiciels que l'on peut mettre à jour :
`apt list --upgradable`{{execute}}

Et puis, si besoin (mais je vous propose de ne pas le faire pour garder les mêmes versions que moi), on peut mettre à jour avec :
`apt upgrade NOM_PAQUET`

## Naviguer dans les dossiers
Vous vous êtes sûrement dit "Mais comment est-ce possible qu'on n'ait pas d'interface graphique ? Il manque pas un truc ?"
En fait, oui, il manque un "truc" : l'affichage graphique. Mais tout le système est là ! L'affichage c'est juste pour faire joli. Nous en tant que geeks chevronnés, on n'a pas besoin de jolies couleurs et d'icônes en forme de dossier...

**À tout moment** le terminal se trouve "dans un dossier". On l'appelle le dossier de travail. Et vous pouvez voir son chemin complet en tapant la commande suivante :
`pwd`{{execute}}

`pwd` signifie 'print working directory" (affiche le dossier de travail)

Et là, vous y voyez ceci :

```
\home
```

C'est similaire au chemin **C:\home** de Windows.

Nous sommes donc dans le dossier principal "\" puis dans le sous dossier home.

Nous pouvons lister ce qui se trouve dans ce dossier actuel, en tapant la commande

`ls`{{execute}}

"ls" vient de "list", on liste donc le contenu.

Vous y voyez donc, toujours au format texte, les fichiers et dossiers se trouvant dans ce fichier.

Bien, maintenant, changeons de dossier ! Normalement, on aurait qu'à cliquer avec la souris sur un autre dossier. Mais ici, on n'a pas d'interface graphique... donc on va changer notre dossier de travail tout simplement !

Et pour cela, voici venue la commande :

`cd /`{{execute}}

On demande ici de changer de dossier, et on donne le "/". On lui dit donc : change le dossier en /

Vous voyez dès lors que le **prompt** change et affiche `root@cyberini:/#` contrairement à `root@cyberini:/home#`. Le système nous indique en fait depuis le début dans quel dossier nous nous trouvons !

Faison à nouveau ls : 
`ls`{{execute}}

Vous y voyez cette fois beaucoup de dossiers et fichiers. Et devinez quoi : il y a **home** ! Car, pour rappel nous étions avant dans **/home**. Donc en listant ce qu'il y a dans **/**, on y trouve **home**.
Pour revenir dedans, il suffit d'entrer :

`cd /home`{{execute}}

Mettant, il reste à comprendre une dernière chose : chemin relatif et chemin absolu.

Un chemin est absolu lorsqu'il commence par **/**. C'est comme dire, sous Windows, C:\mondossier\etc

Un chemin est relatif, si l'on se base au dossier de travail. Si l'on est par exemple dans C:\mondossier, on peut cliquer sur etc directement. En somme, on peut se rendre dans les sous dossiers. Sous linux c'est pareil.

On peut donc créer un dossier :

`mkdir mondossier`{{execute}}

puis se rendre dedans, soit par le chemin relatif:

`cd mondossier`{{execute}}

ou par le chemin absolu :

`cd /home/mondossier`{{execute}}

La différence est principalement la rapidité. Il faut savoir que pour éviter toute erreur, il est préférable de donner le chemin absolu.

Envie de supprimer un dossier ?

Pas de problème, revenons dans le dossier parent d'abord. Là encore, soit on passe par le chemin absolu : cd /home/, soit on utilise le chemin relatif... Et là, nouvelle commande :

`cd ..`{{execute}}

Ce n'est pas une erreur, sous Linux ".." indique le dossier parent. On dit donc littérallement : remonter dans le dossier parent.
Et là, il faut suivre, on peut donc taper à tout moment "pwd" pour voir ou l'on est, et "ls" pour voir ce qu'il y a dans le dossier.
Puis on peut utiliser le chemin relatif pour supprimer le dossier avec la commande appropriée :

`rmdir mondossier`{{execute}}

La même procédure avec chemin relatif et absolu s'applique avec les **fichiers**.
On utilise touch pour créer un fichier (au lieu de mkdir) et rm pour en supprimer un (au lieu de rmdir).

Essayez :

`touch monfichier.txt`{{execute}}

`ls`{{execute}}

`rm monfichier.txt`{{execute}}

`ls`{{execute}}

Il n'est plus là !

Pour finir, et pour ajouter du contenu au fichier, vous pouvez utiliser l'éditeur en ligne de commande nano :

nano monfichier.txt (remplace touch, car on créé et édite en mêem temps)

CTRL + O et CTRL + X pour sauvegarder et fermer.

On peut le réafficher de la même manière, ou utiliser "cat" pour afficher plus rapidement :

car monfichier.txt
