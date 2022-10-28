# Serveur, Service et Client

Dans ce doc on va démystifier un peu les termes suivants : "serveur", "service" et "client".

> Afin de faciliter la lecture de ce doc, on rappelle que les termes suivants sont des synonymes : "application", "logiciel", "soft", "software", "programme".

![Relation Client/Serveur](./pics/client_server.jpeg)

# Sommaire

- [Serveur, Service et Client](#serveur-service-et-client)
- [Sommaire](#sommaire)
  - [I. Serveur](#i-serveur)
    - [1. Un serveur est une machine](#1-un-serveur-est-une-machine)
    - [2. Un serveur est une application](#2-un-serveur-est-une-application)
  - [II. Client](#ii-client)
    - [1. Client et Serveur](#1-client-et-serveur)
    - [2. Le client est une application](#2-le-client-est-une-application)

## I. Serveur

Le terme serveur, suivant le contexte, peut avoir deux sens bien distincts :

- il peut désigner une machine (physique)
- il peut désigner une application

### 1. Un serveur est une machine

➜ *exemples*

- *"j'ai acheté un serveur"*
- *"mon serveur il envoie la patate"*
- *"MON SERVEUR EST INJOIGNABLE" :(*

➜ **un serveur physique, c'est juste un gros PC**

- la différence avec un gros PC c'est uniquement sa forme, pour être mis dans des armoires prévues à cet effet
- aussi, souvent, il est en permanence connecté à un LAN, voire à Internet
- en terme de perfs, ça envoie + de patate aussi
  - 128 ou 256 Go de RAM dans un serveur c'est pas choquant
  - deux procs 8 coeurs dans une machine pas choquant non plus

➜ **le serveur est la machine qui rend un *service***

- le **service** est l'application qu'on lance derrière un port, qu'un client pourra interroger
- le **service** est une application qui attend derrière un port, elle attend la connexion de clients potentiels

> Une VM peut aussi être appelée un *serveur*. On dit alors que ce *serveur* est *virtuel*.

---

Pour concrétiser un peu le truc dans vos esprits, quelques images.

Un serveur de face :

![Serveur - Front](./pics/server_front.jpg)

Un serveur de dos, prenez le temps de repérer la connectique : vous connaissez déjà quasiment tout (alim, USB, réseau Ethernet, etc.). C'est vraiment juste un gros PC.

![Serveur - Back](./pics/server_back.jpg)

Et une ***"armoire"*** ou ***"rack"*** ou ***"baie"***, faite pour accueillir des serveurs :

![Serveur - Rack](./pics/server_rack.jpg)

### 2. Un serveur est une application

➜ *exemples*

- *"mon serveur Web c'est un Apache"*
- *"mon serveur de base de données c'est du sale"*
- *"mon serveur FTP rame frer :'("*

➜ **dans ce cas, on précise quel type de serveur c'est, quel type d'application**

- dans les exemples : "serveur web", "serveur SSH", "serveur de jeu", "serveur DHCP", "serveur DNS", etc.

➜ **un serveur, dans ce contexte, ça désigne l'application qui rend le *service***

- on définit le mot *service* plus bas

Donc il parfaitement possible et pas choquant de dire : *"j'ai installé un **serveur** web sur mon nouveau **serveur** de 64Go de RAM"*.  
Ca fait deux fois "serveur", mais employé dans ses deux sens différents.

➜ **TRES IMPORTANT : un serveur est une application qui ATTEND**

- le serveur attend la connexion de clients
- l'application tourne "dans le vide" tant que personne ne s'y connecte
- quand quelqu'un se connecte au serveur, le serveur lui rend un service

> Par exemple, toujours le même exemple, un serveur Web attend que quelqu'un vienne l'interroger en lui parlant en HTTP. Une fois qu'un client se connecte au serveur Web, alors, à ce moment, le serveur Web travaillera activement pour donner la page HTML que le client à demandé.

## II. Client

Le mot client a lui aussi plusieurs sens :

- le client du client/serveur (physique)
- le client qui désigne l'application qui permet d'accéder à un service

### 1. Client et Serveur

**Le client c'est l'entité qui va consommer les services qui tournent sur des serveurs.**

Ainsi, on peut désigner par client un humain et son smartphone, une fois qu'il est connecté à un réseau quelconque.

Un client, ou "client final" c'est donc l'entité physique qui consomme le service. Le PC, le smartphone, la tablette, whatever.

### 2. Le client est une application

**Le mot *client* désigne aussi l'application qui permet au *client final* (physique) de se connecter à un service.**

> Ainsi, par exemple, pour se connecter à un serveur Web, il faut un client Web (c'est un cas particulier le client Web, car on l'appelle plus communément *navigateur web*.)

Comme pour l'application désignée par le terme *"serveur"*, l'application désignée par le terme *"client"* se voit toujours compléter du type de client.

Il faut un client Web (Firefox) pour accéder à un serveur Web (Apache).  
Il faut un client FTP (FileZilla) pour accéder à un serveur FTP (vsftpd).  
Il faut un client SSH (la commande `ssh`) pour se connecter à un serveur SSH (OpenSSH).  
Etc.

![Error 500](./pics/error_500.jpg)