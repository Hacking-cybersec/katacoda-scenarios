## Gestion des mises à jour
Bien souvent, il convient de faire une mise à jour du dépôt APT pour obtenir la liste des derniers paquets à installer.
En français, cela signifie qu'il y a par exemple une application MonLogiciel qui est passé en version 2. On demande donc au système de nous chercher les informations sur les versions de ces logiciels. 
Pour ce faire, on tape la commande suivante :
`apt-get update`{{execute}}

**Note :** bien souvent, on tapera "`sudo`" avant de taper cette commande. `Sudo` permet de dire "exécute cette commande **en tant qu'administrateur**". Pourquoi ? parce qu'il peut y avoir **plusieurs utilisateurs sur un même système** et tout le monde n'a pas le droit de tout changer, sinon il risque d'y avoir des soucis. Imaginez comme si c'était à l'école, avec les élèves possédant chacun leur compte, et l'enseignant ayant aussi le sien. Seul l'enseignant à les droits d'administrateur pour modifier des choses importantes. Ce compte administrateur s'appelle aussi "root" sous Linux !
Si l'on vous dit que vous n'êtes pas "root", c'est que vous n'êtes pas administrateur...

Et même s'il n'y a personne d'autre que nous sur le système, il faut savoir que sous Linux, on peut "associer des comptes" à des logiciels !
On peut par exemple demander à ce que MonLogicielNonAutorise soit utilisable avec le compte "nonautorise"...

Bref. Vous avez de ce fait vu le système chercher des mises à jour de paquets.
Parfait ! Continuons.

Maintenenant, et si besoin, nous pouvons mettre à jour concrètement un logiciel (ou plusieurs) grâce à la dernière version en notre connaisssance.

On peut d'abord observer la liste des logiciels que l'on peut mettre à jour :
`apt list --upgradable`{{execute}}

Et puis, si besoin (mais je vous propose de ne pas le faire pour garder les mêmes versions que moi), on peut mettre à jour avec :
`apt upgrade \[Nom\]`

## Naviguer dans les dossiers
Vous vous êtes sûrement dit "Mais comment est-ce possible qu'on n'ait pas d'interface graphique ? Il manque pas un truc ?"
En fait, oui, il manque un "truc" : l'affichage graphique. Mais tout le système est là ! L'affichage c'est juste pour faire joli. Nous en tant que geeks chevronnés, on n'a pas besoin de jolies couleurs et d'icônes en forme de dossier...

**À tout moment** le terminal se trouve "dans un dossier". On l'appelle le dossier de travail. Et vous pouvez voir son chemin complet en tapant la commande suivante :
`pwd`{{execute}}

`pwd` signifie 'print working directory" (affiche le dossier de travail)

Et là, vous y voyez ceci :

```
```

Pour ce faire, entrez la commande suivante dans le Terminal (vous pouvez cliquez dessus pour l'entrer automatiquement) :

`recon-ng`{{execute}}

Une fois recon-ng lancé, nous pouvons lancer l'un de ses nombreux modules comme `whois_pocs`.
Utilisons donc ce module (à taper une fois entré dans l'interface recon-ng) :

`modules load recon/domains-contacts/whois_pocs`{{execute}}

**ASTUCE :** vous pouvez voir tous les modules disponibles en tapant `modules load[ESPACE]` suivi de deux fois la touche `TABULATION`.

Une fois entré dans le module concerné, définissons la cible avec la commande suivante :

`options set SOURCE google.com`{{execute}}

Il reste à exécuter le module :

`run`{{execute}}

Après quelques secondes, vous pourrez apercevoir le résultat suivant (non exhaustif) :
```
[...]
[*] [contact] Tracy Weaver (tracyweaver@google.com) - Whois contact
[*] URL: http://whois.arin.net/rest/poc/RRV2-ARIN
[*] [contact] Vamseedhar Reddyvari Raja (vamzee@google.com) - Whois contact
[*] URL: http://whois.arin.net/rest/poc/VITAL21-ARIN
[*] [contact] Ben Vitale (vitale@google.com) - Whois contact
```

Les contacts trouvés sont automatiquement ajoutés dans la base de données de recon-ng.
Nous pouvons les voir en tapant la commande suivante :

`show contacts`{{execute}}

Nous venons de récupérer une liste publique de contacts que Google et ses collaborateurs ont mentionné dans les enregistrements whois. 

Maintenant, à vous de jouer ! Essayez avec un autre domaine ! (PS: tous les domaines ne retournent pas de résultats, et les domaines hors ".com" peuvent ne pas fonctionner, car l'outil utilise le registre Internet ARIN (américain))

Envie d'aller plus loin ? Essayez le module recon/companies-multi/whois_miner qui récupère encore plus d'informations en utilisant un nom d'une entreprise comme "Facebook".

## Aspects juridiques
Les exemples montrés sont tous légaux et récupèrent uniquement des données publiques accessibles. Il vous appartient cependant de prendre en considération que l'utilisation de certains outils ou modules sur des sites ou personnes pour découvrir volontairement des informations confidentielles peut engager votre responsabilité.
