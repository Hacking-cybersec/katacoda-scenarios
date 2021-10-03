## Lister des services et trouver des vulnérabilités
Nous passons à l'étape du scanning réseau. Dans celle-ci, le hacker éthique va tenter de lister des services actifs sur des machines cibles.

L'un des outils les plus **populaires** pour ce faire est `Nmap` (Network mapper). 

Sortons d'abord de recon-ng si ce n'est pas déjà fait, avec la commande `exit`{{execute}}

Nmap s'utilise en ligne de commande de la façon suivante : 

`nmap scanme.nmap.org`{{execute}}

Cet exemple est sans risque. Nmap propose volontairement l'adresse `scanme.nmap.org` pour comprendre le fonctionnement de l'outil "en vrai".

Voici un exemple d'affichage :

```
Starting Nmap 7.80 ( https://nmap.org ) at 1970-01-01 20:15 CEST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.16s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 997 filtered ports
PORT     STATE  SERVICE
80/tcp   open   http
443/tcp  closed https
8080/tcp closed http-proxy

Nmap done: 1 IP address (1 host up) scanned in 10.79 seconds
```

Nmap vient donc de trouver que l'hôte répondant à scanme.nmap.org (d'adresse IP **45.33.32.156**) possède **un port ouvert** et **2 ports fermés**.
Le port ouvert est le port **80** (open) qui correspond au service HTTP.

Essayons d'en savoir plus sur le service qui est actif sur ce port :

`nmap scanme.nmap.org -p80 -sV`{{execute}}

Cette commande demande à Nmap de ne scanner que le port 80 (**-p80**) et de chercher activement les versions des services (**-sV**).

Voici un exemple de résultat renvoyé :

```
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
```

On en déduit donc que sur le port **80** de la machine **45.33.32.156** répondant au nom de **scanme.nmap.org** se trouve le service Apache version **2.4.7**

Essayons à présent de savoir si cette version possède des vulnérabilités connues :
`nmap scanme.nmap.org --script vulners -p80 -sV`{{execute}}

Le résultat suivant s'affiche (non exhaustif) :

```
CVE-2021-26691  7.5     https://vulners.com/cve/CVE-2021-26691
CVE-2017-7679   7.5     https://vulners.com/cve/CVE-2017-7679
CVE-2017-3167   7.5     https://vulners.com/cve/CVE-2017-3167
```

Le service apache est donc potentiellement vulnérable à plusieurs attaques. 

On peut par exemple apprendre que le service Apache peut être terminé à distance (https://vulners.com/cve/CVE-2021-26691) mettant par la même occasion tout éventuel site hebergé sur le serveur **hors ligne**.

Pour aller plus loin : `Nikto` est un scanneur de vulnérabilités web. Il va chercher automatiquement des vulnérabilités sur le site web visé. Voici un exemple de commande : `service apache2 start && nikto -h localhost`{{execute}} (scan du site local par défaut) 

## Aspects juridiques
Le scan des ports est considéré comme illégal dans plusieurs pays. Techniquement, vous devez avoir **l'autorisation préalable** de le faire. Ici, sur scanme.nmap.org, nous l'avons explicitement. De même que sur nos propres serveurs.