# Anonymat en ligne

Cours bonus sur l'identité et plus exactement **l'anonymat en ligne.**

Je vous avais aguiché avec un titre "*Darkweb/Deepweb et notions autour du VPN*".  
C'tait pas mensonger, mais après démystification des termes, notre sujet est devenue l'anonymat en ligne au sens large.

![Stop being tracked](./pics/stop_being_tracked.jpg)

On va donc parler :

- du réseau tor ("Darkweb")
  - c'est le coeur du sujet abordé dans ce cours
  - ce sera la notion la plus développée
- des VPNs
- de la notion de proxy
- et on comparera ces trois solutions en terme d'anonymat et de confidentialité

# Sommaire

- [Anonymat en ligne](#anonymat-en-ligne)
- [Sommaire](#sommaire)
- [I. Deepweb](#i-deepweb)
- [II. DarkWeb](#ii-darkweb)
  - [1. Vocabulaire](#1-vocabulaire)
  - [2. Intro au réseau Tor](#2-intro-au-réseau-tor)
    - [A. Internet](#a-internet)
    - [B. Le Web](#b-le-web)
    - [C. Le réseau Tor](#c-le-réseau-tor)
  - [3. A quoi et a qui ça sert](#3-a-quoi-et-a-qui-ça-sert)
  - [4. Un point sur la censure du Web](#4-un-point-sur-la-censure-du-web)
  - [5. Appréhension technique du réseau Tor](#5-appréhension-technique-du-réseau-tor)
    - [A. Intro technique](#a-intro-technique)
    - [B. Visite du web classique avec Tor](#b-visite-du-web-classique-avec-tor)
    - [C. Visite de *hidden services*](#c-visite-de-hidden-services)
    - [D. Le chiffrement au sein du réseau Tor](#d-le-chiffrement-au-sein-du-réseau-tor)
    - [E. Onion routing](#e-onion-routing)
  - [6. Casser l'anonymat et la confidentialité de Tor](#6-casser-lanonymat-et-la-confidentialité-de-tor)
    - [A. Lors de la visite d'un hidden service](#a-lors-de-la-visite-dun-hidden-service)
      - [➜ Position 1](#-position-1)
      - [➜ Position 2 3 4 5 6 7](#-position-2-3-4-5-6-7)
      - [➜ Position 8](#-position-8)
      - [Résumé](#résumé)
    - [B. Lors de la visite du web classique](#b-lors-de-la-visite-du-web-classique)
      - [➜ Position 1](#-position-1-1)
      - [➜ Position 2](#-position-2)
      - [➜ Position 3](#-position-3)
      - [➜ Position 4](#-position-4)
      - [Résumé](#résumé-1)
  - [7. Résumé](#7-résumé)
- [III. VPN](#iii-vpn)
  - [1. LAN](#1-lan)
  - [2. Internet](#2-internet)
  - [3. VPN](#3-vpn)
    - [A. Fonctionnement et anonymat](#a-fonctionnement-et-anonymat)
  - [B. Confidentialité](#b-confidentialité)
  - [4. Notion de confiance](#4-notion-de-confiance)
    - [A. La douce époque du marketing agressif](#a-la-douce-époque-du-marketing-agressif)
    - [B. Monter son propre VPN](#b-monter-son-propre-vpn)
- [IV. Proxy](#iv-proxy)
- [V. Comparaison](#v-comparaison)
  - [1. Visite classique du Web](#1-visite-classique-du-web)
  - [2. Visite classique du Web avec proxy](#2-visite-classique-du-web-avec-proxy)
  - [3. Visite du Web avec un VPN](#3-visite-du-web-avec-un-vpn)
  - [4. Visite du Web avec Tor](#4-visite-du-web-avec-tor)
  - [5. Visite d'un hidden service tor](#5-visite-dun-hidden-service-tor)

# I. Deepweb

Le *DeepWeb* est un terme ***bien bien bullshit*** pour désigner tout ce qui n'est pas annexé par les moteurs de recherche.

Toute page isolée, c'est à dire une page à laquelle on accède pas de façon directe, en cliquant sur un lien accessible à tous, appartient à cette catégorie.

Donc par exemple, tout ce qui est accessible en donnant un mot de passe : *DeepWeb*. Tout ce qui est généré au moment où vous le visitez : *DeepWeb*. Etc.

Quelques exemples :

- votre fil d'actu facebook
  - protégé par password + généré quand vous le visitez
- votre fil d'actu de n'importe quel réseau social enfet
- n'importe quelle page protégée par un password
- la consultation de votre boîte mail en ligne
- etc.

Le terme désigne quelque chose de réel, mais bon, c'est quoi ce nom quoi. Ca n'a rien de mystique on s'arrête de suite.

**BREF ce cours n'a pas pour but de s'intéresser à ce terme *bullshit*, passons au vif du sujet.**

> On pourrait étendre la définition de DEBILE aux sites Web non exposés publiquement sur Internet je suppose. Genre l'application de Jean-Michel du service de comptabilité. Accessible que depuis le réseau de la boîte. DEEPWEB.

➜ **Go next.**

# II. DarkWeb

## 1. Vocabulaire

Le ***DarkWeb*** est... **encore un terme bien *bullshit***. Tout le monde sera ravi de vous expliquer que le web c'est un iceberg gngngngngnngnnnnn.

Attendez je sors mon canon à images *bullshit* :
*
![Bullshit Bullshit Bullshit Bullshit Bullshit Bullshit Bullshit Bullshit](./pics/iceberg.jpeg)

---

➜ ***DarkWeb* est un terme vulgaire pour désigner de façon quasi exclusive le 🧅 *réseau Tor***, que nous appellerons donc dans la suite par son vrai nom.

## 2. Intro au réseau Tor

On va remettre les mots "Internet" et "Web" à leur place respective avant de continuer.

### A. Internet

➜ **Internet c'est le réseau physique.** C'est les machines + les câbles qui permettent de relier lesdites machine entre elles.  
Internet c'est donc l'infrastructure physique qui vous permet de joindre un serveur à l'autre bout de la planète en un instant.

On trouve des tonnes de cartes plus ou moins justes en ligne. Ca donne au moins une idée :

![Carte de l'Internet](./pics/internet_map.jpg)

Ce réseau Internet est maintenu debout par des entreprises. Il existe des entreprises locales à chaque pays qui se chargent de ça à l'échelle de leur pays. C'est le cas d'Orange en France.

### B. Le Web

➜ **Le Web c'est tout ce qui existe par dessus Internet et qui constitue l'environnement dans lequel on évolue lorsqu'on dit vulgairement que on est "sur internet".**

C'est à dire : des serveurs Web qui parlent l'HTTP, le protocole DNS qui résout les noms de domaines pour nous éviter à utiliser les adresses IP, etc.

Des vidéos de chats, des memes, tout ça. Ca c'est le web.

Aller sur un site en `http://` c'est consommer le Web. Envoyer un mail c'est consommer le Web. Tous les trucs que fait un utilisateur lambda (= un moldu), ça relève du Web.

**Le Web repose sur l'Internet pour fonctionner.**

> Si ça parle à certains : Internet c'est L1 (physique), L2 (Ethernet, MAC) et L3 (IP), alors que le Web c'est L4 (TCP et UDP) et +.

**Bien qu'ayant été créé autour de valeurs comme la neutralité ou la liberté, le Web a aujourd'hui bien dérivé.**

En effet, les fournisseurs d'accès et les gouvernements, entités travaillant de concert, ont une mainmise totale sur la façon dont le réseau fonctionne.

### C. Le réseau Tor

![Is this a VPN](./pics/is_this_a_vpn.jpg)

Le 🧅***réseau Tor***🧅 c'est :

- **un réseau de machines**, connectées entre elles grâce au réseau internet
  - la liste de ces machines est connue, il n'y a rien d'opaque ici
- **entretenu par des bénévoles** : n'importe qui peut héberger un noeud du réseau Tor
  - un *noeud* c'est une machine, un PC, un serveur, peu importe
  - tous les jours il y'a des nouveaux *noeuds*, et d'autres qui s'en vont
- **complètement transparent** dans son fonctionnement
  - les protocoles utilisés par les *noeuds* Tor pour communiquer sont tous open-source
  - on connaît l'identité de la personne qui est derrière chaque machine du réseau Tor
  - **TOUTES** les infos au sujet du réseau Tor sont accessibles facilement et publiquement
- **un réseau ouvert** à la connexion de n'importe qui, à n'importe quel client
  - aucune restriction n'est imposé aux clients
  - **en vérité, il n'y aura JAMAIS de restriction pour l'accès au réseau Tor car c'est justement l'objectif : proposer un accès à un réseau libéré des contraintes**

En résumé, le *réseau Tor*, plus communément et sobrement appelé 🧅 *Tor* 🧅 est une alternative au Web, qui utilise aussi Internet comme réseau physique.

> 🧅🧅🧅 Les oignons c'est le logo de *Tor*, y'a une raison technique, on détaille ça dans [la partie dédiée à l'explication un peu plus technique de *Tor*](#5-appréhension-technique-du-réseau-tor).

🧅***Tor* est une alternative au Web. Cette alternative au Web est libre, ouverte, neutre, décentralisée et garantit une forte sécurité des échanges.**

## 3. A quoi et a qui ça sert

➜ On peut faire deux choses avec 🧅*Tor* :

- **visiter le Web classique**, en passant par le ***réseau Tor***
  - donc on visite les même sites que d'habitude genre `www.ynov.com`
  - la différence est un anonymat plus fort qu'avec une connexion classique (on va détailler ça)
- **visiter des *hidden services***
  - ce sont visuellement des sites web classiques
  - sauf qu'ils ne sont pas accessibles avec un navigateur web classique
  - il est *strictement nécessaire* de passer par le *réseau Tor* pour y accéder
  - la visite de ces sites garantit un anonymat très fort
  - **un *hidden service* est un site Web hébergé au sein-même du *réseau Tor***

**En résumé, utiliser le 🧅*réseau Tor* permet de garantir un fort anonymat en ligne, ainsi que la garantie d'une forte confidentialité des échanges.**

> Ca veut dire quoi "anonymat fort" ? On va s'y intéresser tout au long de ce document. Quoiqu'il arrive, aucun système n'est infaillible, et personne ne peut vous garantir techniquement une sécurité à 100% (que ce soit en terme d'anonymat, ou de confidentialité de vos données).

---

➜ **Qui utilise *Tor* ?** Les gens qui ont des choses à cacher, qui veulent faire des trucs illégaux, qui veulent masquer leur identité en ligne. Evident voyons.

**Wait wait, illégal ?** Bah oui ! Genre quoi ?

- vendre de la drogue, c'est illégal en France
- aller sur le web, c'est illégal en Chine
- communiquer sur l'état du pays, c'est illégal dans pas mal de dictatures

**Ca permet aux uns, privilégiés, d'acheter leur coke, et aux autres, journalistes en zone de guerre, de simplement pouvoir communiquer avec le reste du monde.**

> [Vous trouverez en commentaires de cette page des témoignages de gens qui utilisent Tor de façon légitime en expliquant leurs raisons.](https://blog.torproject.org/how-has-tor-helped-you-we-need-your-stories)

➜ **Savoir si 🧅*Tor* est une bonne ou mauvaise chose est une question purement morale.** C'est un réseau complètement libre et décentralisé, sans contraintes, tout y est possible.

L'outil n'est pas bon ou mauvais en soit, mais c'est l'utilisation qu'on en fait qui peut avoir une intention bienveillante ou malveillante.

**Au contraire, 🧅*Tor* se veut complètement neutre.**

> **Allez tit exemple pour les français**. Sachez que la SNCF effectue des pratiques illégales en augmentant le prix de vos billets s'ils détectent que vous êtes "intéressés" par un billet donné. En repérant que vous avez effectué plusieurs fois la même recherche par exemple. 🧅*Tor* permet de se prémunir de ce genre de pratiques mises en place par des commerçants fallacieux.

## 4. Un point sur la censure du Web

![Censorship](./pics/censorship.jpg)

➜ **Le Web est né avec l'idée de créer un réseau libre, décentralisé, où tout le monde pourrait proposer et accéder librement à de l'information. C bo non ?**

**Bon aujourd'hui, le Web n'a plus rien de libre, ni de neutre.** Cette définition colle aujourd'hui bien mieux à *Tor* qu'au web classique.

La raison en est simple : Internet et le Web sont maintenus en vie par des boîtes privées (comme Orange en France), qui sont en relations étroites avec les gouvernements, et qui peuvent appliquer certains mesures techniques sur ces réseaux, afin de modifier leur comportement.

**C'est donc une question exclusivement politique.**

---

➜ **Ainsi la censure est notamment mise en place au niveau DNS** : vous vous voulez accéder à un site qui porte un nom, vous allez donc demander à votre Box l'adresse IP qui correspond à ce nom.

Lorsque vous demandez un nom de domaine, votre fournisseur d'accès le voit, et il agit comme il entend avec la requête : il peut la bloquer par exemple. Ainsi vous ne connaîtrez jamais l'adresse IP qui correspond au nom du site que vous voulez visitez, et vous ne pourrez donc jamais visiter ledit site.

> C'est possible car les requêtes DNS passent en clair sur le réseau, elles ne sont pas chiffrées. Donc votre routeur (la box chez vous) connaît le nom de tous les sites que vous visitez, et peut choisir de vous répondre ce qu'elle veut.  
En France la liste des noms de domaine censurés est entretenue par l'armée. Elle n'est pas publique. La reconstituer est illégal.  

---

> Il existe d'autres moyens de censure Internet, sur lesquels nous n'allons pas nous étendre maintenant.

🧅🧅🧅 **Aucune de ces mesures de censure n'est applicable si l'on utilise le *réseau Tor*. Ce que nous allons prouver en abordant son fonctionnement d'un point de vue plus concret et technique.**

![Freedom silence](./pics/freedom_silence.jpg)

## 5. Appréhension technique du réseau Tor

> Il est **strictement nécessaire** d'avoir appréhendé les concepts abordés lors du [premier cours de crypto](../intro_crypto/README.md), en particulier le chiffrement, afin de pouvoir assimiler comment fonctionne 🧅*Tor*.

### A. Intro technique

**Le 🧅*réseau Tor* c'est simplement des machines qui ont installé l'application *Tor* et qui ont signalé qu'elles souhaitaient faire partie du réseau.**

> N'importe qui peut télécharger le logiciel *Tor*. et l'installer sur son PC, ou plus souvent un serveur. Y'a des membres du réseau Tor c'est juste des Raspberry hehe.

➜ On appelle ***noeud Tor*** une machine du *réseau Tor*.

Pour comprendre comment ça marche on va étudier les deux façons d'utiliser le *réseau Tor* : visite du web classique en passant par *Tor* d'une part, et visite de *hidden services* d'autre part.  
On s'intéressera dans un deuxième temps au chiffrement au sein de Tor.

### B. Visite du web classique avec Tor

**Quand un client veut visiter le Web en passant par le 🧅*réseau Tor***, concrètement :

- le client utilise un navigateur Web capable d'utiliser Tor
  - comme le [Tor Browser](https://www.torproject.org/download/) (basé sur Firefox, qui est un outil libre et open-source)
- il se connecte à un site comme `www.ynov.com`
- son navigateur va élire un ***circuit Tor*** : il va choisir 3 *noeuds Tor*
- les requêtes vers `www.ynov.com` passeront d'abord par ce *circuit*, par ces 3 *noeuds Tor* avant d'atteindre le serveur `www.ynov.com`
- les réponses de `www.ynov.com` vers le client passeront aussi par ce circuit

➜ **Premier aspect donc : des intermédiaires entre le client et la destination.**  
Ces intermédiaires sont au nombre de 3, ce sont des *noeuds Tor* choisis par le client.  

➜ Ces trois *noeuds* choisis par le client sont appelés ***circuit Tor***.

![Circuit Tor](./pics/circuit.png)

Pour le serveur de destination, `google.com` dans l'exemple ci-dessous, la source des messages est le *noeud Tor* de sortie : **l'identité du client est ainsi masquée**.

![Visiter le web classique avec Tor](./pics/visit_classic_web.png)

### C. Visite de *hidden services*

La visite d'un *hidden service* est très similaire. Sauf que :

- l'adresse du site est différente de ce qu'on voit d'habitude
  - c'est un hash qui se termine par `.onion`
  - les adresses des *hidden services* ne sont donc pas vraiment lisibles par des humains contrairement aux noms de domaine qui sont faits pour être *human-readable*
  - un exemple : `a3xduj55x2j27l2qy3c6tcetykyfxbjbafinex4i3ywddzphkbrd3jyd.onion`
- le site n'est accessible qu'avec un navigateur Tor
- le client établit un circuit, mais le serveur qui porte le site aussi, il y a donc 6 machines intermédiaires au lieu de 3
- le client et le serveur se rejoignent au sein du *réseau Tor* à un point de rendez-vous (il est vraiment appelé "*rendezvous point*" en anglais)

➜ **Dans le cas des *hidden services* on a donc encore plus d'intermédiaires que lorsqu'on visite le web classique.**

![Visiter un hidden service Tor](pics/visit_hidden_service.png)

> Monter un *hidden service* c'est l'affaire de quelques minutes à peine, j'ai fait la démo en cours.

### D. Le chiffrement au sein du réseau Tor

Tous les messages qui circulent au sein du *réseau Tor* sont chiffrés. Plus précisément :

- **si on visite le web classique**
  - le trafic est normalement déjà chiffré entre le client et le serveur grâce à HTTPS
  - il sera rechiffré du client jusqu'au dernier *noeud Tor* de son circuit
- **si on visite un *hidden service***
  - le trafic est complètement chiffré du client jusqu'au serveur qui porte le *hidden service*

De plus, dès qu'un message part de la machine du client à destination du réseau *Tor*, en plus d'être chiffré, il est découpé en petits blocs de taille fixe.  
Cela rend le trafic *Tor* complètement uniforme : des blocs de taille égale,  complètement chiffrés.

![Les messages qui circulent dans Tor sont chiffrés, et de même taille](./pics/same_length.png)

**Donc si quelqu'un regarde ce qui circule entre deux *noeuds Tor*, il ne voit que des blocs de la même taille et complètement chiffrés.**

### E. Onion routing

Venons-en aux oignons 🧅.

**Le terme *onion routing* désigne le routage et le chiffrement qui est mis en palce au sein du *réseau Tor*.**

Le concept est le suivant :

- lorsqu'un client choisit un *circuit*, il échange aussi des clés de chiffrement
  - il définit une paire de clé de chiffrement avec chaque *noeud* du *circuit*
  - dans le schéma ci-dessous les clés sont dénommées `K1`, `K2` et `K3`
- chaque message que le client envoie, il le chiffre 3 fois
  - une fois avec chaque clé
  - 3 clés donc triple chiffrement
- chaque *noeud* va déchiffrer ce qu'il peut
  - chaque *noeud* va enlever une couche de chiffrement
- le dernier *noeud* voit alors la requête en clair et l'envoie à la destination

Le chiffrement mis en place est analogue à un oignon, d'où le nom 🧅.

**En bref : les requêtes envoyés dans un circuit Tor son triplement chiffrées. A chaque fois que le message travers un *noeud* du *circuit*, le *noeud* enlève une couche du chiffrement.**

**Autre point important : chaque *noeud* n'a conscience que de la source immédiate et de la destination immédiate du message.**  
Ainsi le premier *noeud* n'a aucune idée du contenu du message.  
Le dernier *noeud* n'a aucune idée de l'identité du client ou même du premier *noeud*.

![Onion Routing](./pics/onion_routing.png)

> Il faut encore que le serveur réponde au client après ! C'est le même principe.Lors du transit de la réponse du serveur, chaque *noeud* va de nouveau chiffrer la requête avec sa clé. Ainsi, la réponse reçue par le client est elle aussi triplement chiffrée. Il peut alors la déchiffrer avec les 3 clés en sa possession.

## 6. Casser l'anonymat et la confidentialité de Tor

Pour étudier l'anonymat et la confidentialité en place lors de l'utilisation du *réseau Tor*, et si on peut les casser, il nous faut étudier les deux cas possibles séparément : visite du web classique en passant par Tor et visite de *hidden service*.

Un peu de vocabulaire pour ça :

- un *Tor node* c'est une machine du *réseau Tor*
- un *Guard Node* c'est une machine du *réseau Tor* qui est choisie comme première machine de son circuit par un client
- un *Exit Node* c'est une machine du *réseau Tor* qui est choisir comme dernière machine de son circuit par un client

![Guard and Exit Nodes](./pics/guard_exit_node.png)

### A. Lors de la visite d'un hidden service

![Positions possibles d'un hacker lors de la visite d'un hidden service](./pics/hidden_service_hack.png)

#### ➜ Position 1

Le hacker est entre le client et le Guard Node, ou a le contrôle du Guard Node.  
Il sait seulement que le client utilise le réseau Tor, mais n'a aucune info supplémentaire.

#### ➜ Position 2 3 4 5 6 7

Le hacker est entre le Guard Node et le *noeud* du milieu, ou a le contrôle d'un *noeud* du milieu.

N'importe qui entre les autres *noeuds* ou en possession d'un des *noeuds* ne voit que des blocs chiffrés de la même taille (sans source ou destination apparentes).

#### ➜ Position 8

Le propriétaire du *hidden service* sait qu'un client du *réseau Tor* visite son site (il ne sait pas qui).

#### Résumé

**Lors de la visite d'un *hidden service* l'anonymat est quasi-total.** Même si l'on prend le contrôle de plusieurs *noeuds* du chemin, l'anonymat est conservé.

### B. Lors de la visite du web classique

![Positions possibles d'un hacker lors de la visite du Web classique](./pics/classic_web_hack.png)

#### ➜ Position 1

Le hacker est entre le client et le Guard Node, ou a le contrôle du Guard Node.  
Il sait seulement que le client utilise le réseau Tor, mais n'a aucune info supplémentaire.

#### ➜ Position 2

Le hacker est entre le Guard Node et le *noeud* du milieu, ou a le contrôle du *noeud* du milieu.  

Il ne voit que des blocs chiffrés de la même taille (sans source ou destination apparentes).

#### ➜ Position 3

Le hacker est entre le *noeud* du milieu et l'Exit Node ou a le contrôle de l'Exit Node.

Il sait qu'un client essaie de visiter un site web classique en passant par le réseau Tor. Il sait quel site web est visité. Il ne sait pas quel client a voulu le visiter.

> Son rôle est d'effectuer la requête, puis de la renvoyer dans l'autre sens dans le circuit.

#### ➜ Position 4

Le hacker est entre l'Exit Node et le serveur de destination, ou il a le contrôle du serveur de destination.

Il sait qu'un client visite le serveur. Il peut savoir, s'il connaît la liste des IPs des *noeuds Tor* (qui est publique) que c'est un client du *réseau Tor*.

#### Résumé

Un hacker présent sur le *Guard* ou le *Exit Node* ou quelques infos, mais rien de bien concluant. Pour permettre de savoir quel client fait quoi, il faudrait que le hacker prennent le contrôle à la fois du *Guard* et du *Exit Node*.

## 7. Résumé

**Le *réseau Tor* est un réseau de machines décentralisé, libre et ouvert.** N'importe qui peut faire partie de ce réseau.

Le but est de fournir **un accès à un Web complètement libéré des contraintes**, ceci en garantissant un fort anonymat et une forte confidentialité des échanges.

On peut **visiter le Web classique en passant par Tor**, ce qui garantit un meilleur anonymat et une meilleure confidentialité de nos données.

On peut aussi **visiter des *hidden services*** : ce sont des serveurs Web hébergés au sein-même du *réseau Tor*. L'accès à un *hidden service* se fait dans un anonymat et une confidentialité extrêmement forts.

**Tout cela repose uniquement sur des applications libres et open-source, ainsi que des protocoles ouverts.**

Cela permet toutes sorte de trafic légal, mais aussi des choses illégales. Illégal ne signifie pas malveillant, **la discussion autour de la légitimité de l'existence de *Tor* est un débat morale et éthique.**

> Pour la réf, c'est [Edward Snowden](https://fr.wikipedia.org/wiki/Edward_Snowden) sur le meme juste en dessous.

![Edward Snowden](./pics/snowden.jpg)

# III. VPN

Ok ! On va pouvoir parler des VPNs, notions un peu plus simple à comprendre que le fonctionnement du *réseau tor*.

*VPN* c'est pour *Virtual Private Network*. Pour comprendre cette notion, il faut bien comprendre ce que c'est un réseau local (ou *LAN*). Il faut aussi avoir saisi comment, depuis un LAN, on accède à un autre réseau comme Internet.

## 1. LAN

➜ **Un *LAN* c'est juste des machines connectées localement entre elles.**

Il faut : des clients (PC, smartphones, etc.) et un switch (à la maison, c'est la box qui fait office de switch).

Reste plus qu'à relier tout ce beau monde avec des câbles (ou du WiFi) et **BIM** ça fait un *LAN* ou *réseau local*.

On dit qu'on est "connecté au réseau local" quand on est connectés physiquement à d'autres machines proches de nous.

## 2. Internet

➜ **Pour que, depuis un *LAN*, on ait accès à d'autres réseau comme Internet, il faut être connecté à un routeur** (à la maison, c'est aussi la box qui fait ça).

**Quand le routeur est connecté à Internet, il a une IP publique.** Cette IP publique c'est l'identité de tous les membres du LAN aux yeux d'Internet.

Peu importe quel membre du LAN va sur Internet, c'est l'IP publique unique du routeur qui est vue comme source, du point de vue des autres machines d'Internet.

## 3. VPN

### A. Fonctionnement et anonymat

➜ **Se connecter à un *VPN* c'est simplement utiliser une application qui nous permet de simuler l'accès à un *LAN* sans y être physiquement.**

Ainsi, quand vous vous connectez à un *VPN*, vous vous connectez simplement à un *LAN*.  
Sauf que contrairement à un *LAN* classique, où il faut physiquement être présents au même endroit, avec un *VPN*, on peut être dans un *LAN* à distance.

➜ Le *serveur VPN* c'est la machine qui accueille les clients et qui leur donne accès à ce LAN.

La classe non ?

> Pour les gamerzzz old-school, vous avez peut-être connu Hamachi ou Tunngle. Ces trucs permettaient de lancer des jeux et jouer en LAN, mais à travers Internet, bien pratique à l'époque. C'était juste du *VPN*.

**Ainsi, une fois connecté au *VPN*, toutes les requêtes vers Internet vont d'aaaaabord passer par le réseau *VPN* (qui est un simple LAN), et sortir par le routeur de ce LAN.**

---

➜ Prenons l'exemple d'une requête envoyée vers `google.com` une fois connecté à un *VPN*. Le trafic va donc dans l'ordre :

- de votre PC à votre routeur 1 (la box)
- de votre routeur 1 au routeur 2 auquel est connecté le serveur *VPN*
- du routeur 2, vers `google.com`

**Donc votre identité en ligne n'est plus l'IP publique de votre routeur 1 (votre box) mais à la place, votre identité est celle de l'IP publique du routeur 2 du serveur *VPN*.**

L'utilisation d'un *VPN* permet donc de garantir un certain anonymat en ligne *via* l'utilisation d'un système centralisé (tout repose sur le serveur *VPN*).

![VPN anonymat](./pics/vpn_hommer.jpg)

## B. Confidentialité

➜ En plus de permettre l'accès à un *LAN* distant, **les *VPN* mettent aussi en place du chiffrement afin de garantir la confidentialité des données.**

Ainsi, toutes les requêtes qui transitent entre le client et le *serveur VPN* sont chiffrées. **Cela garantit une confidentialité des données lors du transit entre le client et le serveur.**

## 4. Notion de confiance

➜ **La notion de confiance est prépondérante lors de l'utilisation d'un VPN.** En effet, l'utilisation d'un VPN suppose que le client a une confiance totale dans le fournisseur VPN.

En effet, le chiffrement des données est mis en place entre le client et le serveur. **Ainsi, le *serveur VPN* a accès aux données telles qu'elles auraient circulé normalement sans VPN.**

Aussi, l'anonymat est en place pour le serveur de destination. **Mais le serveur VPN a parfaitement connaissance de quel client visite quel site.**

➜ On voit donc que pour les deux aspects garantis par l'utilisation d'un *VPN*, l'anonymat et la confidentialité, cela repose totalement sur la bonne foi du fournisseur *VPN*.

### A. La douce époque du marketing agressif

Il est devenu récemment à la mode de souscrire à une offre VPN pour "protéger ses données en ligne". Oui je te vois NordVPN gngngnnn.

➜ **Bon qu'on soit clairs au sujet de ces fournisseurs de *VPN* :**

- les IPs publiques de ces fournisseurs *VPN* (comme NordVPN & co) sont connues
  - ça veut dire que regarder Netflix en passant par NordVPN, c'est bientôt de l'histoire ancienne
  - car ces IPs vont être blacklistées (c'est déjà le cas, sur Youtube aussi pour certaines)
- anonymat et confidentialité
  - vous êtes tout de suite catégorisés comme des utilisateurs de *VPN* aux yeux du Web
  - le fournisseur du *VPN* a une mainmise totale sur vos données
- internet c'est la jungle
  - la plupart des gros acteurs jouent des coudes sévères pour trouver toujours des nouveaux moyens de faire du fric avec le web
  - prenez le en compte dans vos jugements

> De façon générale, allumez-vos neurones quand vous subissez un marketing agressif qui crée des besoins. Si on vous crée un besoin, c'est suspect, par essence. Pas forcément malveillant, mal intentionné, c'est même peut être une bonne chose. MAIS ça doit susciter la réflexion.

➜ **Si on résume d'un point de vue très terre-à-terre ce que font les gens qui souscrivent à ce genre d'offres** : vouloir garantir son anonymat et la confidentialité de ses données en divulgant son identité et en donnant accès à toutes ses données à une entreprise privée qui a pour objectif de faire du business.

➜ Ca doit allumer des lumières là-haut normalement, quand on vit à l'époque où la moindre donnée se monnaye.

### B. Monter son propre VPN

**WAIT WAIT le concept du *VPN* n'est pas DU TOUT à jeter pour autant.**

Le fait de pouvoir se connecter à un LAN sans y être physiquement, ça reste le feu total.

Ca permet par exemple à un administrateur système de se connecter au réseau de sa boîte à distance, et de bosser sur les serveurs comme s'il y était. C'était très pratique en temps de COVID :)

Le *hic* du *VPN* c'est la notion de confiance. Mais si on monte son propre *VPN*, alors la notion de confiance disparaît, car on maintient nous-mêmes le serveur.

> Notez que ça prend moins d'une heure à un administrateur système de monter un *VPN* maison avec par exemple [OpenVPN](https://openvpn.net/) ou [Wireguard](https://www.wireguard.com/).

![Get a VPN](./pics/get_a_vpn.jpg)

# IV. Proxy

Ok dernière notion : le *proxy*. Ca va être très rapide.

Un *proxy* c'est simplement un intermédiaire entre un client et sa destination. Le client est libre de choisir un serveur intermédiaire, par lequel transiteront ses requêtes avant d'atteindre la destination.

> Ca se configure en quelques clics dans n'importe quel navigateur Web par exemple.

L'utilisation d'un *proxy* permet d'accéder à un certain anonymat, car c'est le *proxy* qui effectue toutes les requêtes à notre place.

Vous pouvez en installer un vous-mêmes sur un serveur quelque part sur Internet. Ou il existe des tonnes de listes de *proxies* gratuits sur internet par-ci par-là.

Aucun chiffrement n'est mis en place.

# V. Comparaison

On va aller du "moins sécurisé" au "plus sécurisé".

> **Qu'on soit clairs au sujet d'un truc** : peu importe la méthode utilisée, si vous allez sur facebook où y'a votre prénom et votre nom, vous êtes cramés c'est tout. Tant mieux si ça paraissait obvious.

## 1. Visite classique du Web

![Web classique](./pics/compare_classic_web.png)

Un PC avec un navigateur Web, connecté à Internet.

Connexion classique à un site Web, on est en 2021 et on est pas des bêtes alors c'est du HTTPS.

Avec HTTPS, y'a une bonne couche de chiffrement déjà, les données sont confidentielles jusqu'au serveur.

On oublie pas qu'à chaque site visité, vous effectuez une requête DNS pour connaître l'IP du site. Cette requête DNS n'est jamais.

> En fait elles peuvent être chiffrées, ça s'active dans le navigateur; Ayez une navigation saine et activez-le :) [Tuto pour Firefox ici](https://support.mozilla.org/fr/kb/dns-via-https-firefox).

Côté anonymat c'est zéro obviously :

- votre fournisseur d'accès sait tout ce que vous faites
- un hacker dans votre LAN sait tout ce que vous faites
- le serveur de destination connaît votre identité (= l'IP publique de votre box)
- chiffrement : HTTPS classique
- anonymat : 0

> Par "sait tout ce que vous faites" on entend : connaître la source et la destination des messages, leur longueur, et quelques autres infos. Le contenu des message est chiffré grâce à HTTPS.

Quand on parle d'un hacker dans votre LAN, c'est pas de la science-fiction hein. Bon OK, chez vous peinards dans le canapé, assez improbable. Quand vous connectez au WiFi public de la gare, c'est BEAUCOUP plus probable. Hihi.

## 2. Visite classique du Web avec proxy

![Web classique avec proxy](./pics/compare_proxy.png)

Un PC avec un navigateur Web, connecté à Internet.

On configure le PC pour utiliser un *proxy*.

En vrai ça change pas grand chose. Le serveur de destination ne connaît plus votre identité mais c'est à peu près tout. Bon début on dira.

- votre fournisseur d'accès sait tout ce que vous faites
- un hacker dans votre LAN sait tout ce que vous faites
- le serveur de destination ne connaît pas votre identité
- chiffrement : HTTPS classique
- anonymat : un peu mieux

## 3. Visite du Web avec un VPN

![VPN](./pics/compare_vpn.png)

Un PC avec un navigateur Web, connecté à Internet.

On configure le PC en installant une application pour se connecter à un serveur *VPN* + on obtient un certificat auprès du fournisseur du *VPN* (pour pouvoir s'y connecter).

On monte d'un gros cran là. Toutes les requêtes sont chiffrées entre le client et le serveur *VPN*. Ainsi un potentiel hacker ou le fournisseur d'accès Internet ne voient que des paquets chiffrés, qui partent vers Internet.

Ils peuvent déduire assez vite que vous utilisez un *VPN*. A la limite, c'est un *VPN* connu, et ils savent lequel c'est, car ses IPs publique sont connues et répertoriées.

Ensuite, le serveur *VPN* lui, il a accès à toutes vos données. Se pose alors la question de la confiance.

Pour le serveur de destination, c'est le *VPN* qui fait les requêtes, donc on a un bon anonymat. Le serveur de destination peut déduire, en connaissant éventuellement l'IP de votre *VPN*, que vous utilisez un *VPN*.

- votre fournisseur d'accès ne sait rien
  - à part que vous utilisez un *VPN*
- un hacker dans votre LAN ne sait rien
  - à part que vous utilisez un *VPN*
- le serveur de destination ne connaît pas votre identité
  - à part que vous utilisez un *VPN*, si c'est un *VPN* connu
- chiffrement : HTTPS classique + chiffrement du client au serveur *VPN*
- anonymat : bien mieux
- toute la sécurité (anonymat comme confidentialité) repose sur la confiance accordée au propriétaire du *VPN*

## 4. Visite du Web avec Tor

![Web avec Tor](./pics/compare_tor.png)

Un PC avec un navigateur Web capable de se connecter au *réseau Tor*, connecté à Internet.

On grimpe encore d'un cran.

L'utilisation du réseau *Tor* met en place un triple chiffrement, en utilisant des chiffrements forts. Aussi, les messages chiffrés sont fragmentés en bloc de même taille ce qui rend le trafic complètement uniforme (même la longueur des messages est masqueée).

Aux yeux d'un potential hacker dans le LAN ou de votre fournisseur d'accès c'est la mierda, c'est le pire possible : toutes les trames sont full chiffrées et font la même taille. Pas la moindre info à en tirer. Sauf : vous êtes connecté au *réseau Tor*.

Pour le serveur de destination, votre identité est complètement masquée par le biais des trois intermédiaires de votre *circuit Tor*. Il peut éventuellement savoir que vous utilisez *Tor*.

> A noter que pour la machine du milieu, et le *Exit Node*, votre identité est masquée aussi. Donc le serveur de destination, il est pas prêt de l'avoir...

Aucune notion de confiance en un acteur unique ici : *Tor* est un réseau décentralisé.

> "Décentralisé" n'est pas la réponse à tout, mais on parle ici d'un réseau décentralisé mature, composé d'un grand nombre de *noeuds*, fonctionnant avec des principes complètement transparents.

- votre fournisseur d'accès ne sait rien
  - à part que vous utilisez *Tor*
- un hacker dans votre LAN ne sait rien
  - à part que vous utilisez *Tor*
- le serveur de destination ne connaît pas votre identité
  - à part que vous utilisez *Tor*
- chiffrement : HTTPS classique + triple chiffrement du client au *réseau Tor*
- anonymat : très fort

## 5. Visite d'un hidden service tor

![Hidden service](./pics/compare_hiddenservice.png)

Bon bah là. Hihi.

Le trafic est chiffré de bout en bout, c'est à dire que rien, à aucun moment, n'est en clair, entre le client et le serveur de destination.

La seule chose qui circule entre les deux, du client, à la destination, c'est des paquets de même taille, complètement chiffrés.

On est dans un échange où personne ne connaît l'identité de personne. Le client et le serveur se donne un point de rendez-vous, tout le temps différent, afin de communiquer au sein du *réseau Tor*.

Pour le potentiel hacker et votre fournisseur d'accès, c'est pareil que juste avant : ils ne voient rien si ce n'est que vous utilisez le *réseau Tor*.

Le serveur de destination n'a aucune idée de votre identité, et il ne veut même pas que vous connaissiez la sienne (vous ne connaîtrez jamais l'IP publique du *hidden service* lorsque vous le visitez).

- votre fournisseur d'accès ne sait rien
  - à part que vous utilisez *Tor*
- un hacker dans votre LAN ne sait rien
  - à part que vous utilisez *Tor*
- le serveur de destination ne connaît pas votre identité
  - et vous ne connaissez pas la sienne
- chiffrement :
  - triple chiffrement du client au *réseau Tor*
  - triple chiffrement du serveur au *réseau Tor*
- anonymat : quasi total

> Au fait, *Tor* ça rame de ouf. Bah oui triple chiffrement, au moins 3 intermédiaires... La sécurité a toujours un prix en terme de performances.

![Who would win ?](pics/who_would_win.jpg)