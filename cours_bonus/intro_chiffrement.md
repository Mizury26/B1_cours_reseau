# Intro Crypto

- [Intro Crypto](#intro-crypto)
- [Crypto Intro](#crypto-intro)
  - [I. Encoding](#i-encoding)
    - [What ?](#what-)
    - [Examples](#examples)
    - [Why ?](#why-)
  - [II. Hashing](#ii-hashing)
  - [III. Chiffrement](#iii-chiffrement)
    - [1. Chiffrement symétrique](#1-chiffrement-symétrique)
    - [2. Chiffrement asymétrique](#2-chiffrement-asymétrique)
      - [A. Signature](#a-signature)
      - [B. Echange confidentiel](#b-echange-confidentiel)
      - [C. Cas réel](#c-cas-réel)
    - [3. Symétrique ou asymétrique](#3-symétrique-ou-asymétrique)

## I. Encoding

### What ?

L'*encoding* ou *encodage* est le fait d'utilise un *code* pour changer la forme d'un message. C'est une opération très peu coûteuse en performances  

**Encoder un texte n'est pas une sécurité : il n'y a aucune notion de secret.**

> La crypto étant la science du secret, on est un peu hors sujet ici. Je préfère néanmoins parler d'encodage ici pour démystifier le terme, et ne pas le confondre avec ce qui suivra (hashing et chiffrement).

Obligé de le citer ici, parce qu'il est trop confondu avec le reste. 

### Examples

- binaire (base2)
- décimal (base10)
- octal (base8)
- hexadécimal (base16)
- base64 (très utilisé en info pour stocker des petites données)
  - pendant le cours utilisation de `base64` et `base64 -d`
  - **la base64** n'est **PAS** du chiffrement, m'kay ?
- ASCII (base 128)

### Why ?

Gagner de la place, économiser du trafic réseau, améliorer les performances.

Aussi et surtout, permettre un standard pour stocker ou faire transiter des infos (comme le binaire pour les disques durs mécaniques).

![We have base64 encryption n_n](./pic/we-have-base64-encryption.jpg)

## II. Hashing

Le *hashing* est le fait d'utiliser une fonction mathématique, appelée fonction de hachage, afin de calculer *l'empreinte* ou *hash* d'un fichier ou d'une chaîne de caractère.
Cette action est par définition **irréversible**.

Ces fonctions de hachage possèdent plusieurs propriétés :

- **fonctions à sens unique**
  - on ne peut pas, à partir d'un *hash*, remonter à la donnée entrée dans la fonction de hachage
- **non prédictibles**
  - un petit changement dans la donnée d'entrée résulte en un changement total du *hash*
  - difficile de trouver des *collisions* : deux entrées différentes qui donneraient le même *hash*
- aussi, un hash doit être **facile et rapide à calculer**

Exemples de fonctions de hachage :

- [MD5](https://en.wikipedia.org/wiki/MD5) (obsolète)
- [SHA-1](https://en.wikipedia.org/wiki/SHA-1)
- [SHA-2](https://en.wikipedia.org/wiki/SHA-2)

Il est possible de calculer rapidement un *hash* depuis n'importe quel langage, y compris `bash` :

```bash
$ echo 'test' | md5sum
d8e8fca2dc0f896fd7cb4cb0031ba249  -

$ echo 'test' | sha1sum
da39a3ee5e6b4b0d3255bfef95601890afd80709  -

$ echo 'test' | sha256sum
f2ca1bb6c7e907d06dafe4687e579fce76b37e4e93b7605022da52e6ccc26fd2  -
```

## III. Chiffrement

![Encrypt all the things](./pic/encrypt-all-the-things.jpg)

Le chiffrement permet d'assurer le transfert ou le stockage sécurisé d'une information.

Le chiffrement est le fait d'utiliser un **algorithme de chiffrement** ainsi qu'une **clé de chiffrement** afin de transformer un fichier ou chaîne de caractère en un message "codé" ou plutôt, chiffré. Un message chiffré est illisible, et ne permet pas retrouver le message original, sauf pour les détenteurs de la **clé de déchiffrement**.  

Le chiffrement permet d'assurer le transfert ou le stockage sécurisé d'une information.

Il existe deux types de chiffrements :

- **symétrique**
  - la clé de chiffrement et la clé de déchiffrement sont les mêmes
- **asymétrique**
  - la clé de chiffrement et de déchiffrement sont différentes

**Point vocabulaire**

- "*chiffrer*" = transformer un *message* en *ciphertext* avec un *algo de chiffrement* et une *clé*
- "*déchiffrer*" = transformer un *ciphertext* en son *message original*, lorsque l'on connaît l'*algo* et la *clé* utilisée
- "*décrypter*" = démarche de hacker consistant à retrouver le *message original* d'un *ciphertext* sans avoir connaissance de la *clé* et/ou de l'*algo* utilisé pour le *chiffrement*
- "crypter" = chiffrer sans avoir connaissance de l'algo ou de la clé ?...
  - **STRICTEMENT IMPOSSIBLE. PAR DEFINITION.**

> Voir **l'excellent https://chiffrer.info** à ce sujet.

On appelle désigne souvent par le terme **tunnel chiffré** le fait d'échanger des clés avec quelqu'un afin d'être en mesure de discuter de façon sécurisée.  
Une fois les clés échangées, on dit que "le tunnel est établi". Ainsi les deux parties peuvent échanger des infos de façon sûre.

### 1. Chiffrement symétrique

Les chiffrements symétriques sont des chiffrements simples et **performants**. On peut citer :

- [chiffrement par décalage](https://fr.wikipedia.org/wiki/Chiffrement_par_d%C3%A9calage)
  - simple décalage de lettres dans l'alphabet
  - la clé est le nombre de lettres dont on décale dans l'alphabet
- d'autres chiffrements bien plus robustes qu'un chiffrement par décalage existent, comme [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)
  - il existe plusieurs variantes d'AES
  - AES est utilisé dans la plupart des communications chiffrées nécessitant performances et sécurité (comme les connexions HTTPS)

> L'inconvénient d'une telle méthode est qu'elle nécessite l'échange préalable d'une clé, **avant** l'établissement d'un tunnel de communication chiffré.

### 2. Chiffrement asymétrique

Le chiffrement asymétrique repose sur des algorithmes qui ont la particularité d'utiliser des clés différentes pour le chiffrement et le déchiffrement des données.

Ainsi, lors de la génération initiale de clés pour pouvoir mettre en place le chiffrement, deux clés sont générées. Tout ce que chiffre l'une d'entre elles, l'autre peut le déchiffrer.

Il est possible de mettre en place deux choses avec un chiffrement asymétrique :

- **signature**
  - garantir l'authenticité et l'identité d'un participant lors d'un échange
- **chiffrement**
  - garantir la confidentialité d'un message lors de son transit

On peut citer par exemple [RSA](https://en.wikipedia.org/wiki/RSA_cryptosystem) ou encore [EC](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography).

#### A. Signature

> En crypto, les exemples sont souvent donnés avec Alice, Bob et Eve.  
Alice et Bob sont les deux participants à la communication. Ces noms ont été choisis car ça fait A et B les initiales.  
Eve c'est pour "eavesdropping" : écouter au porte. Eve représente un potentiel hacker.

Supposons deux participants Alice et Bob.

Alice génère sa paire de clés. L'une est dite *publique* (peu importe laquelle), l'autre est alors dite *privée*.

Alice garde sa clé *privée* `cléPrivA` et ne la partagera jamais avec personne.  
Alice distribue sa clé *publique* `cléPubA`, y compris à Bob.

Alice peut alors envoyer un message à Bob en le chiffrant avec sa clé privée `cléPrivA`.  
Si Bob peut peut déchiffrer le message, **alors il a la garantie que c'est bien Alice qui l'a envoyé : seule la clé privée `cléPrivA` d'Alice a pu chiffrer ce message**.

**Alice a donc *signé* son message : elle a prouvé son *identité* à Bob.**

![Schéma signature](./pic/sign.png)

#### B. Echange confidentiel

Supposons deux participants Alice et Bob.

Alice génère sa paire de clés. L'une est dite *publique* (peu importe laquelle), l'autre est alors dite *privée*.

Alice garde sa clé *privée* `cléPrivA` et ne la partagera jamais avec personne.  
Alice distribue sa clé *publique* `cléPubA`, y compris à Bob.

Bob peut alors chiffrer un message avec la clé publique `cléPubA` d'Alice, et l'envoyer à Alice.  
**Seule Alice, détenteuse de la clé privée `cléPrivA`**, pourra déchiffrer le message.

**Bob a donc garanti la *confidentialité* du message qu'il voulait envoyer à Alice.**

![Schéma secret](./pic/secret.png)

#### C. Cas réel

Si on récapitule les deux exemples ci-dessus concernant la signature et le chiffrement avec un algo asymétrique :

1. Alice génère une paire de clés
2. elle garde la privée, donne la publique à tout le monde, y compris Bob
3. Alice peut alors signer ses messages
4. tout le monde, y compris Bob, peut lui envoyer des messages confidentiels

Dans un cas réel, Bob fait de même de son côté, et donc distribue sa clé publique à tout le monde.

**Ainsi, chacune des deux parties, Alice et Bob, peuvent à la fois signer leurs messages et s'échanger des messages confidentiels.**

![Schéma signed secret](./pic/signed_secret.png)

### 3. Symétrique ou asymétrique

Les deux types de chiffrement, symétrique ou asymétrique, peuvent résulter en des chiffremetns très forts, de robustesse équivalente.

Mais il y a deux aspects (principalement) qui vont permettre de s'orienter sur l'un plutôt que l'autre :

- **performances**
  - les chiffrements symétriques demandent beaucoup BEAUCOUP moins de ressources
  - on préférera toujours utiliser les chiffrements symétriques pour cette raison
- **problème avec le chiffrement symétrique** : l'échange de la clé
  - cependant il y a un soucis. La clé est la même pour chiffrer et déchiffrer. Il est donc nécessaire de la partager de façon sécurisée... avant l'établissement du tunnel de chiffrement :/
  - on peut éventuellement procéder à un échange physique de la clé
  - ou alors (et c'est souvent le cas en réalité), **on utilise un chiffrement *asymétrique* pour échanger une clé *symétrique***

![What part did you not understand ? :c](./pic/what-part-of-encrypt-all-the-things-did-you-not-understand.jpg)
