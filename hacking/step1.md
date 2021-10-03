## Qu'est-ce que la reconnaissance ?
La reconnaissance est l'une des étapes les plus importantes. Elle consiste à trouver des informations sur une cible. Cela se fait principalement à travers Internet, mais il est aussi possible d'écouter des communications ou de récupérer des documents physiques.

## La reconnaissance en pratique
L'outil `recon-ng` est dédié à cette étape et apporte beaucoup de fonctionnalités. Par exemple, il permet de découvrir le **propriétaire d'un site web** via les enregistrements **whois**. Ces informations sont notamment fournies par l'exploitant lors de la création d'un nom de domaine auprès d'un [Registraire de nom de domaine](https://fr.wikipedia.org/wiki/Registraire_de_nom_de_domaine). Et bien qu'il existe des solutions de protection de données personnelles dans les enregistrements whois, la plupart des enregistrements contiennent des données accessibles **publiquement**.

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
