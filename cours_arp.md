# ARP

- [ARP](#arp)
- [Concept](#concept)
- [Trames ARP](#trames-arp)
- [Cas concret](#cas-concret)
- [Table ARP](#table-arp)
  - [Cas de la passerelle](#cas-de-la-passerelle)

# Concept

ARP (*Adress Resolution Protocol*) est un protocole qui permet de faire le lien entre les adresses MAC et les adresses IP.

➜ Comme tout protocole en réseau , ARP vient répondre à une problématique :

- un PC se trouve dans un LAN et possède une IP
- il souhaite contacter une autre machine de son LAN, dont il connaît l'IP
- pour communiquer avec cette machine, vu qu'elle est dans son LAN, il **DOIT** connaître sa MAC

**ARP est donc le protocole qui va permettre à notre PC de déterminer l'adresse MAC d'un destinataire de son LAN dont il connaît l'IPs.**

➜ Le concept est simple :

- une machine A a besoin de joindre une machine B en connaissant son IP
- A demande à tout le monde sur le réseau qui porte l'IP de B
- B reçoit le message et informe A que c'est lui qui porte cette IP

# Trames ARP

Il y a deux principales trames dans ARP :

- ***ARP request***
  - envoyé par un client qui souhaite connaître la MAC d'une IP donnée
  - la trame est envoyée en broadcast
  - on appelle aussi cette trame *Who-has*
    - en effet, la trame se traduit par "Who has IP X.X.X.X, tell Y.Y.Y.Y" : "Qui a l'IP X.X.X.X, répondez à l'IP Y.Y.Y.Y"
- ***ARP reply***
  - réponse à un *ARP request*
  - un client renseigne son adresse MAC à un autre client

# Cas concret

```schema
             switch
           +---------+
   +-------+         +-------+
   |       +---------+       |
   |                         |
   |                         |
   |                         |
   |                         |
+--+--+                   +--+--+
|     |                   |     |
|     |                   |     |
|     |                   |     |
+-----+                   +-----+
client1                   client2
```

| Machine   | Adresse MAC          | Adresse IP |
|-----------|----------------------|------------|
| `client1` | `11:11:11:11:11:11`  | `10.1.1.1` |
| `client2` | `22:22:22:22:22:22` | `10.1.1.2` |

On suppose que `client1` veut envoyer un message à `client2` (par exemple, un `ping`). Les deux machines vont alors automatiquement procéder à un échange ARP :

➜ Dans l'ordre, les trames envoyées :

- un *ARP request* envoyé de `client1` vers tout le monde dans le réseau
- un *ARP reply* envoyé de `client2` à `client1`

| Trame            | Adresse MAC source  | Adresse MAC destination | Signification                         |
|------------------|---------------------|-------------------------|---------------------------------------|
| 1. *ARP request* | `11:11:11:11:11:11` | `ff:ff:ff:ff:ff:ff`     | "Who has `10.1.1.2` ? Tell `10.1.1.1` |
| 2. *ARP reply*   | `22:22:22:22:22:22` | `11:11:11:11:11:11`     | "`10.1.1.2` is at `22:22:22:22:22:22` |

➜ L'adresse `ff:ff:ff:ff:ff:ff` s'appelle *adresse de broadcast*. Elle est unique, sa valeur est toujours `ff:ff:ff:ff:ff:ff`.  
Si un switch reçoit une trame avec `ff:ff:ff:ff:ff:ff` pour destination, il aura pour rôle d'envoyer cette trame à TOUT LE MONDE sur le réseau. Ceci assure que la personne concerné recevra bel et bien le message.

➜ Le `client2` (comme tout le monde sur son réseau) reçoit cette trame envoyée en broadcast par `client1` et voit qu'elle lui est destinée : cela veut dire que `client1` souhaite connaître la MAC associée à son IP `10.1.1.2`. `client2` répond alors directement à `client1` en lui donnant l'info qu'il voulait.

**Une fois l'échange effectué, `client1` et `client2` connaissent l'adresse MAC de l'autre.**

# Table ARP

➜ **Une fois l'échange ARP effectué, chaque client stocke dans sa table ARP l'info récupérée.**

> Dans l'exemple donné plus haut, on a par exemple `client1` qui a enregistré que `10.1.1.2` possède l'adresse MAC `22:22:22:22:22:22` dans sa table ARP.

➜ Toutes les machines possèdent une table ARP. Une entrée dans la table ARP est temporaire : il est nécessaire de réitérer les échanges ARP régulièrement.

> La table ARP est aussi appeleée "table de voisinnage" car elle contient tous nos "voisins" (*neighbors* en anglais) : elle contient l'adresse MAC de tous les gens du même réseau que nous avec qui on a déjà communiqué. Elle est aussi appelée "cache ARP" car c'est la table qui "cache" les informations ARP.

## Cas de la passerelle

Si vous êtes connectés à un réseau qui vous permet d'accéder à d'autres réseaux, par exemple Internet, vous avec au moins une entrée dans votre table ARP : **l'adresse de votre passerelle**.  

En effet, pour communiquer avec l'extérieur, vous passez par votre passerelle.  
Or il est indispensable de connaître son adresse MAC si on veut lui envoyer des messages, car elle est dans notre LAN.

Donc pour envoyer des messages à la passerelle pour qu'elle les envoie sur Internet, il faut connaître son adresse MAC.