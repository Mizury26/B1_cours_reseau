# La notion de "port" en réseau

Ici on va clarifier plusieurs termes :

- carte réseau (ou interface réseau)
- réseau local (ou LAN)
- port
- firewall (ou pare-feu)

# Sommaire

- [La notion de "port" en réseau](#la-notion-de-port-en-réseau)
- [Sommaire](#sommaire)
- [1. Intro](#1-intro)
- [2. Client et serveur](#2-client-et-serveur)
- [3. Analogie serveur](#3-analogie-serveur)
- [4. Cas réel](#4-cas-réel)
- [5. Voir les connexions établies](#5-voir-les-connexions-établies)
- [6. Le firewall](#6-le-firewall)

> Pour bien appréhender cette partie, il faut être déjà familier avec [les notions de Serveur, de Service et de Client](../serveur/README.md).

# 1. Intro

➜ **Un *port* est une porte d'entrée ou de sortie, sur une interface réseau.**

> Attention, ici on ne parle PAS des ports Ethernet, ou des ports USB, ou je ne sais quoi. Les ports dont on parle ici ne sont PAS physiques.

➜ Un *port* permet de se connecter à une autre machine, et d'échanger des données avec.  

Chaque carte réseau possède 65 536 *ports* TCP et autant en UDP (c'est comme ça hihi).  
Il existe donc ~135k ports sur chaque interface réseau.

➜ "Ouvrir" un port c'est lancer une application qui utilise ce port

- on lance une application/un logiciel
- elle est placée derrière l'un des ports d'une carte réseau

# 2. Client et serveur

**Il existe deux types de connexions :**

➜ **les connexions serveur**

- votre machine agit comme un serveur
- votre machine attend la connexion d'un éventuel client
- **on dit que votre machine est en écoute** (ou *listening* en anglais)

➜ **les connexions client**

- votre machine agit comme un client
- votre machine peut donc initier des connexions vers des serveurs

➜ Le principe d'un service réseau, comme un serveur Web, c'est qu'il y a une application qui attend, qui écoute.  
**Plus précisément, cette application écoute sur un *port*.**

Encore dit autrement : lancer un serveur Web, c'est le fait d'exécuter un programme qui comprend le protocole du web (HTTP) et de le placer derrière un port réseau (80/tcp ou 443/tcp par convention).

➜ Les 65 536 *ports* de l'interface réseau de votre machine sont numérotées, de façon unique (le *port* 1, le *port* 2, ..., le *port* 65 536).  
**Quand on lance une application comme un serveur Web, il va se placer derrière l'un de ces *ports*.**

➜ **Pour les deux types de connexion**

- connexion serveur
  - le serveur écoute sur un *port* donné, et attend la connexion d'éventuels clients
- connexion client
  - le client utilise un *port* aléatoire pour se connecter au *port* d'un serveur
  - le client doit connaître le *port* du serveur auquel il veut se connecter

> Les expressions suivantes sont synonymes : "écouter derrière un *port*", "écouter sur un *port*", "être derrière un *port*", "attendre derrière un *port*".

# 3. Analogie serveur

Dans le cas du serveur, représentez-le vous vraiment comme :

- votre machine, le serveur, c'est un terrain
- votre terrain, il a une adresse postale
  - c'est l'adresse IP de la machine
- sur votre terrain, y'a un ou plusieurs hangar(s), avec chacun un nom
  - c'est les cartes réseau de la machine
- y'a 65 536 portes sur chaque hangar
  - 65 536 *ports* sur chaque carte réseau
- vous ouvrez un ptit restau chez vous, dans l'un des hangars, chill comme ça. Vous l'appelez "au plus beau des serveurs Web"
  - le restau, c'est un service
- le restau est dans la pièce derrière la porte numéro 80 du Hangar A
  - c'est l'équivalent du serveur Web qui écoute sur le port 80
- tous les gens du quartier connaissent votre adresse et savent qu'à la porte 80 du Hangar A, y'a un restau
  - les gens connaissent l'IP et le *port* sur lequel joindre votre service
- tous les gens du quartier peuvent venir manger dans votre restau 🔥

Cette analogie est extrêmement juste pour se représenter la notion de *port*.  
Notez le fait que les clients doivent connaître l'adresse et le *port* où tourne le service.

> Par convention, certains protocoles se sont vus associés des numéros de *port*. Par exemple : HTTP c'est *port* 80, HTTPS c'est *port* 443, SSH c'est *port* 22.

---

Mentionnons que, le client de votre restau, avant d'aller chez vous, il est sorti de chez lui. En passant par sa porte d'entrée. **HE OUI.**

> Il est sorti par une porte de chez lui. On en apprend des choses en cours de Linux hein.

**Pareil en informatique : le client ouvre un port random pour se connecter à un serveur.**

# 4. Cas réel

Quand vous connectez à un site web : vous connaissez son adresse IP (ou son nom de domaine, c'est pareil, la notion de nom de domaine et de DNS est hors sujet), et le *port* auquel vous devez vous connecter.

Ainsi, quand on se connecte à `https://www.ynov.com` en fait on se connecte implicitement au *port* 443 sur la machine de destination.  

> Beaucoup d'applications, comme les navigateurs Web, cachent le numéro de *port* auquel on se connecte, parce que madame Michue la moldue n'aime pas voir des numéros sur son écran.

Pour préciser à quel *port* on veut se connecter sur une machine donnée, on utilise la notation `IP:PORT` par exemple `192.168.1.1:80` ou encore `www.ynov.com:443`.

---

Faites le test dans votre navigateur web :

- `https://www.ynov.com` vous donne la page d'YNOV
  - vous avez demandé l'adresse `www.ynov.com`
  - vous avez demandé le *port* 443 (c'est implicite à cause du HTTPS, c'est votre navigateur qui a fait ça)
- `https://www.ynov.com:443` ça revient au même
  - vous avez demandé l'adresse `www.ynov.com`
  - vous avez demandé le *port* 443 explicitement
  - vous voyez que le numéro de *port* est enlevé par votre navigateur pour les yeux des moldus
- `https://www.ynov.com:8888` qui ne donnera rien
  - vous avez demandé l'adresse `www.ynov.com`
  - vous avez demandé le *port* 8888 explicitement
  - le serveur d'YNOV n'écoute pas sur le *port* 8888, donc vous attendrez un moment

> Comme si vous frappiez à la porte 8888 du Hangar d'YNOV. Sauf que dans la pièce derrière cette porte, y'a personne.

# 5. Voir les connexions établies

Vous pouvez utiliser la commande `ss` sur les OS GNU/Linux pour voir les connexions actives. La commande sous MacOS et Windows, c'est `netstat`.

Petit détail sur la commande `ss` vu qu'on est en Linux ici è_é :

```bash
# Liste tous les ports actifs (TCP et UDP)
# -t pour TCP
# -u pour UDP
$ ss -tu

# Liste uniquement les ports en écoute
# Les ports où il y a une application derrière qui attend
# Les ports pour lesquels notre machine est un serveur quoi !
# -l pour listen
$ ss -ltu

# On rajoute souvent deux autres options : -p et -n
# Et on a besoin des droits root pour -p
# Je vous laisse explorer vous-même ce que font ce -p et -n
$ sudo ss -ltunp
```

# 6. Le firewall

Petit big up pour la notion de *firewall*. On profite d'avoir la tête dans les *ports* pour parler du *firewall* !

![Cut here to activate firewall](./pics/firewall_cut_here.jpg)

➜ **Petit rappel de réseau : tout message (*paquet*) sur le réseau possède...**

- une adresse IP source
  - c'est l'adresse de l'émetteur du message, du paquet
- une adresse IP de destination
  - c'est l'adresse du destinataire
- un *port* source
  - c'est le *port* par lequel le message est sorti sur la machine de l'émetteur
- un *port* destination
  - c'est le *port* par lequel doit entre le message sur la machine de destination

---

Venons-en à notre *pare-feu* ou *firewall* en anglais.

➜ **Le *pare-feu* est une application.**

Et ça n'a rien à voir avec un antivirus SVP. Ne confondez pas **SVPPPP**, ça n'a vraiment VRAIMENT rien à voir. Un "*pare-feu*" et un "antivirus" sont deux termes précis et complètement distincts.

➜ Il existe un *pare-feu* sur quasiment toutes les machines du monde (les clients, comme les serveurs).

➜ **Le *pare-feu* permet d'autoriser ou bloquer des connexions réseau.**  

On s'en sert généralement pour bloquer les connexions qui entrent sur une machine (on protège une machine des connexions que peuvent tenter les autres vers elle).  
Mais un *firewall* peut très bien bloquer les connexions sortantes d'une machine (on protège les autres machines, en restreignant les connexionx qu'une machine peut émettre).

> Souvent, un *pare-feu* fonctionne sur un principe de *whitelist* : tout est bloqué, puis on liste explicitement et exhaustivement ce qu'on veut autoriser. Par opposition à la *blacklist* : on autorise tout, et on explicite ce qu'on veut bloquer.

➜ **Le *pare-feu* analyse chacun des paquets que reçoit une machine, et détermine s'il peut rentrer ou non.**  

---

Il peut regarder 4 principaux critères pour savoir si un paquet a le droit d'entrer ou sortir sur une machine : les adresses IP source/destination et les *ports* source/destination.

Par exemple : on peut demander au *firewall* d'une machine de...

- bloquer toutes les connexions entrantes qui viennent d'une adresse IP donnée
  - idéal pour blacklist quelqu'un
- autoriser tout le trafic à destination d'un *port* donné sur la machine
  - idéal pour autoriser des clients à joindre un serveur qui tourne sur notre machine
- bloquer les connexions à la plupart des *ports* d'une machine
  - idéal pour protéger une machine d'éventuelles intrusions
  - on ferme les *ports* où l'on ne désire pas de connexions de la part d'éventuels clients
- bloquer les connexions qu'effectuent une machine vers l'extérieur
  - idéal pour empêcher une machine d'utilise le réseau, ou une partie du réseau
  - on protège ainsi les autres machines du réseau de celle-ci
  - idéal pour empêcher une machine de pouvoir faire nawak, dans l'hypothèse où un hacker en prend possession
  
> Pour compléter l'image avec le hangar étou. **Le *pare-feu* c'est le videur.** No joke. Devant chaque porte y'a un mec : le videur, et c'est lui qui décide si tu rentres ou pas.  
Pour rentrer derrère la porte d'un hangar, faut passer le videur. Et le videur, il a des critères. Si t'as des baskets, tu rentres po.

**Ainsi, l'efficacité d'un *firewall* dépend uniquement de sa configuration : qu'est-ce qu'il autorise ou bloque.**

![Windows Firewall](./pics/windows_firewall.jpg)