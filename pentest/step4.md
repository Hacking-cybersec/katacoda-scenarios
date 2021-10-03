## Rester et se cacher le plus longtemps possible
Cette étape est facultative aussi bien pour le pirate que le hacker éthique qui réalise le test d'intrusion.

En pratique, il s'agit de se garantir un accès futur plus facile. Sans avoir à repasser par la même méthode employée pour s'introduire dans un système. 

Pour cela, le pirate va essayer de mettre en place une **porte dérobée** (backdoor) dans le système. Le nom est bien choisi : il ouvre une "porte" cachée dans le système qu'il pourra utiliser pour y revenir.

Concrètement cette porte correspond par exemple à l'ouverture d'un **port réseau**. Nous ne pouvons pas voir d'exemple ici car le système virtuel est justement protégé contre ce type d'intrusions.

Pour cacher ses traces, le pirate va notamment s'occuper des différents dossiers **logs** présents sur le système.
Vous pouvez les observer en listant le contenu du dossier `/var/logs/` :
`ls -al /var/log/`{{execute}}

Voici un exemple de résultat affiché :
```
drwxr-xr-x  5 root  root   4096 Sep 15 20:43 .
drwxr-xr-x 12 root  root   4096 Sep 15 20:42 ..
-rw-r--r--  3 root  root   9801 Sep 15 20:43 alternatives.log
drwxr-x---  2 root  adm    4096 Sep 15 20:42 apache2
drwxr-xr-x  2 root  root   4096 Sep 15 20:43 apt
-rw-r--r--  6 root  root  58592 Aug 27 09:17 bootstrap.log
-rw-rw----  6 root  utmp      0 Aug 27 09:16 btmp
-rw-r--r--  3 root  root 252926 Sep 15 20:44 dpkg.log
-rw-r--r--  3 root  root   3264 Sep 15 20:43 faillog
-rw-rw-r--  3 root  utmp  29784 Sep 15 20:43 lastlog
drwxr-x---  2 mysql adm    4096 Sep 15 20:43 mysql
-rw-rw-r--  6 root  utmp      0 Aug 27 09:16 wtmp
```

Nous y voyons notamment la date de dernière modification. Et nous pouvons voir le contenu avec la commande cat :

`cat /var/log/apache2/error.log`{{execute}} (il se peut qu'il soit vide ici)

Ce fichier `error.log` affiche notamment les éventuelles erreurs produites par un outil de scanning automatisé, ou par des tentatives diverses d'accès infructueux au site web hebergé sur le serveur.

Le pirate pourra par exemple l'éditer ou le supprimer :

`rm -rf /var/log/apache2/error.log`{{execute}}

Essayez maintenant de retaper la commande car précédente, et vous y verrez une erreur.

Les groupes APT dont nous avons parlé dans la formation sont experts dans ces techniques de maintien d'accès (et connaissent bien d'autres techniques plus sophistiquées).

## Aspects juridiques
Le fait de se "maintenir frauduleusement" dans un système informatisé et évidemment puni au même titre que l'accès en lui-même lorsqu'aucune autorisation n'a été reçue.