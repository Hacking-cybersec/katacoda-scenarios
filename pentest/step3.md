## L'étape critique du test d'intrusion !

Imaginons à présent que nous avons découvert des informations sur une cible avec `recon-ng` et `Nmap`.

Cela nous a permis d'accéder à un fichier mal sécurisé contenant des mots de passe accessibles publiquement.

Disons que nous l'avons déjà récupéré et placé sur notre système.

Il se trouve en fait dans le dossier `/home` dans lequel nous nous trouvons avec le terminal !

Tapez la commande suivante pour lister les fichiers du répertoire home :
`ls /home`{{execute}}

Pour voir le contenu du fichier, tapons la commande :
`cat /home/motdepasse.txt`{{execute}}

Ha ! Le mot de passe n'est pas "en clair" (sinon ce serait trop facile...). Nous allons donc essayer de le "casser" ou "cracker" avec un outil automatisé !

Je vous présente **John The Ripper**, un célèbre outil casseur de mot de passe que nous pouvons utiliser de la manière suivante :

`john /home/motdepasse.txt`{{execute}}

Vous pouvez appuyer sur la touche **ESPACE** pour voir où en est John. Mais après plusieus secondes... plusieurs minutes... voire plusieurs heures ? John ne semble pas trouver le mot de passe. Normal, il utilise le mode **single** par défaut. C'est un mix de combinaisons avec des noms communs, des noms de dossiers, etc.

Nous pouvons donc faire mieux (en imaginant que le mot de passe a été écrit en français) : **utiliser un dictionnaire de mots français**.

Tapez CTRL+C `^C`{{execute ctrl-seq}} pour stopper John. 
Procédons par l'installation du dictionnaire d'abord :
`apt install -y wfrench`{{execute}}

Une fois installé, vous pouvez voir le contenu du dictionnaire avec la commande suivante : 
`cat /usr/share/dict/french`{{execute}}

Bien. Passons aux choses sérieuses, et essayons de casser le mot de passe en nous aidant du dictionnaire :
`john --wordlist=/usr/share/dict/french motdepasse.txt`{{execute}}

Au bout d'une dizaine de secondes... le mot de passe apparaît, je vous laisse le découvrir !

Vous pouvez ensuite voir le mot de passe trouvé avec la commande suivante :
`john --show motdepasse.txt && cat /root/admin.txt`{{execute}}

## Aspects juridiques
Il n'est pas légal de procéder à de telles opérations **sans avoir reçu les permissions nécessaires**. Ici, il s'agit d'un exemple sur nos propres machines. Pour rappel, cette étape du test d'intrusion est celle où l'on accède à un compte ou à un système. C'est donc celle où nous sommes ainsi potentiellement concernés par l'"accès frauduleux" (Article 323 du code pénal).