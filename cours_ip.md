# Manipulation d'adresses IP

- [Manipulation d'adresses IP](#manipulation-dadresses-ip)
- [I. Adresse IP](#i-adresse-ip)
- [II. Calcul d'adressage](#ii-calcul-dadressage)
- [III. Subnetting](#iii-subnetting)

# I. Adresse IP

Une adresse IP se présente sous la forme `10.1.1.50` : c'est une suite de 4 octets, les valeurs allant dont de 0 à 255.

Elle est **toujours** accompagnée d'un **masque de sous-réseau** qui se présente sous une forme similaire à une adresse IP, par exemple `255.255.255.0` ou dans une notation qu'on appelle CIDR : `/24`.

Si on convertit un masque de sous-réseau en binaire, il est **toujours** constitué d'une suite de 1, puis de 0.

Par exemple, `255.255.255.0` se convertit en `1111 1111.1111 1111.1111 1111.0000 0000`. 

Le nombre de 1 dans le masque en binaire détermine la notation CIDR. Ici on a 24 bits à 1, on peut donc aussi dire que ce masque est un `/24`.

# II. Calcul d'adressage

A partir d'une *adresse IP* et d'un *masque de sous-réseau*, on peut déduire :

- l'*adresse du réseau* dans lequel se trouve l'adresse IP donnée
- l'*adresse de broadcast* ("diffusion") de ce réseau LAN
- et enfin le nombre d'hôtes disponibles dans ce réseau LAN

---

A l'aide d'un `ipconfig` ou `ifconfig`, on peut **repérer l'adresse IP d'une machine donnée**.

Nous continuerons avec un exemple, en servant de l'IP privée suivante : `192.168.3.17/22`.  

**1.** `/22` est la *notation CIDR* d'une IP et de son masque. Une autre façon de le dire est :

- adresse IP : `192.168.3.17` ou en binaire `11000000.10101000.00000011.00010001`
- masque de sous-réseau : `255.255.252.0` ou en binaire `11111111.11111111.11111100.00000000`  
  
> Si on a un /22 alors on 22 bits à 1 au début du masque, puis le reste rempli de 0. Un masque est toujours une suite de 1 d'affilée, puis de 0 d'affilée.

**2.** Notons l'un sous l'autre afin de correctement visualiser l'utilisation du masque :

```bash
A. 11000000.10101000.00000011.00010001  (adresse IP)
B. 11111111.11111111.11111100.00000000  (masque de sous-réseau)
```  
  
**3.** Pour **calculer l'adresse de réseau**, il faut regarder les deux lignes en même temps (comme si on appliquait un "masque" à l'adresse IP, vraiment) :

- si la ligne B (le masque) contient un 1, alors on "garde" le chiffre correspondant de la ligne A
- si la ligne B (le masque) contient un 0, alors on "jette" le chiffre correspondant de la ligne A, et on note 0
  
- ici, on obtient :

```schema
                             adresse
        adresse réseau         hôte
   .----------------------..---------.
A. 11000000.10101000.00000011.00010001  (adresse IP)
B. 11111111.11111111.11111100.00000000  (masque de sous-réseau)
C. 11000000.10101000.00000000.00000000  (adresse de réseau)
```

> Une autre façon de le dire, c'est que si le masque c'est un /22, alors on va garder les 22 premiers bits de l'adresse de départ, et remplir le reste avec des 0.

**L'adresse de réseau de `192.168.1.37/22` est `11000000.10101000.00000000.00000000/22` soit `192.168.0.0/22`.**
Elle correspond dans notre exemple au 22 premiers bits de l'adresse IP de départ, suivie de 0. Car c'est un `/22`.  

**4.** Pour **calculer l'adresse de broadcast**, on garde aussi les 22 premiers bits de l'adresse IP, mais cette fois, on comble avec des 1 :

```schema
                             adresse
        adresse réseau         hôte
   .----------------------..---------.
A. 11000000.10101000.00000011.00010001  (adresse IP)
B. 11111111.11111111.11111100.00000000  (masque de sous-réseau)
C. 11000000.10101000.00000000.00000000  (adresse de réseau)
D. 11000000.10101000.00000011.11111111  (adresse de brodcast)
```

**L'adresse de broadcast du réseau `192.168.0.0/22` est `11000000.10101000.00000011.11111111/22` soit `192.168.3.255/22`.
Elle correspond dans notre exemple au 22 premiers bits de l'adresse IP de départ, suivie de 1. Car c'est un `/22`.  

> Une autre façon de le dire, c'est que si le masque c'est un /22, alors on va garder les 22 premiers bits de l'adresse de départ, et remplir le reste avec des 1.

**5.** Souvent (mais pas tout le temps), la *gateway* ou *passerelle* porte l'adresse IP juste avant l'adresse de broadcast :

```schema
                             adresse
        adresse réseau         hôte
   .----------------------..---------.
A. 11000000.10101000.00000011.00010001  (adresse IP)
B. 11111111.11111111.11111100.00000000  (masque de sous-réseau)
C. 11000000.10101000.00000000.00000000  (adresse de réseau)
D. 11000000.10101000.00000011.11111111  (adresse de broadcast)
E. 11000000.10101000.00000011.11111110  (adresse de gateway)
```
  
**6.** Une fois ces notions en tête, on peut **calculer le nombre d'hôtes possibles** :

- notre réseau est un `/22` cela fait donc 10 bits disponibles pour nos adresses d'hôtes (l'IP est constituée de 32 bits, et 22 sont réservés à l'adresse réseau)
- 10 bits disponibles, cela fait 2^10 possibilités, soit 1024 possibilités, **1024 "adresses possibles MAIS"** :
  - l'adresse de réseau n'est pas utilisable : 1023 possibilités
  - l'adresse de brodcast n'est pas utilisable : 1022 possibilités
  - si le réseau possède une gateway, son IP n'est pas libre : 1021 possibilités
- en comptant l'adresse de gateway, on a **1021 adresses disponibles** ("possible" != "disponible")
  
- **NB**
  - la partie `adresse de réseau` ne change **jamais** pour toutes les adresses d'un réseau donné (on le voit bien dans le `5.`)
  - toutes les machines d'un même réseau peuvent communiquer
  - grâce à nos interfaces réseau, on peut porter des IPs, et ainsi être dans un réseau
  - **c'est bien le fait d'avoir une adresse qui nous rend "membre d'un réseau"**  

# III. Subnetting

A l'aide d'un `ipconfig` ou `ifconfig`, on repère l'adresse IP d'une machine donnée : `10.33.3.17/22`.  

**1.** On calcule l'*adresse de réseau* pour cette IP, ainsi que l'*adresse de broadcast*

```schema
                             adresse
        adresse réseau         hôte
   .----------------------..---------.
A. 00001010.00100001.00000011.00010001  (adresse IP)
B. 11111111.11111111.11111100.00000000  (masque de sous-réseau)
C. 00001010.00100001.00000000.00000000  (adresse de réseau)
D. 00001010.00100001.00000011.11111111  (adresse de broadcast)
```


```schema
                             adresse
        adresse réseau         hôte
   .----------------------..---------.
A. 00001010.00100001.00000011.00010001  (adresse IP)
B. 11111111.11111111.11111100.00000000  (masque de sous-réseau)
C. 00001010.00100001.00000000.00000000  (adresse de réseau)
D. 00001010.00100001.00000011.11111111  (adresse de broadcast)
```

Nous avons 10 bits pour notre adresse d'hôte, et 22 bits pour l'adresse de réseau (défini par le masque).  
Avec 10 bits, il y a 2^10 adresses possibles, soit 1024 possibilités.  

En enlevant l'adresse de réseau et l'adresse de broadcast, on a 1024 - 2 = **1022 adresses disponibles**.  

**3.** En décimal, le réseau étudié est `10.33.0.0/22`. A des fins pédagogiques, imaginons que nous avons ce réseau `10.33.0.0/22` à notre disposition, et qu'on souhaite le découper. En admettant que personne ne se trouve actuellement dans ce réseau, on va découper le réseau en plusieurs sous-réseaux, afin d'héberger des machines ayant des fonctions différentes. On veut un réseau pour chacun des groupes suivants :

- 57 PCs
- 12 serveurs
- 26 imprimantes  

On appelle ça du **subnetting** : du *sous-réseautage*. Du découpage de réseau en sous-réseaux quoi !  

**4.** Mise en place du subnetting : on cherche le plus petit réseau dans lequel on peut mettre chacun des équipements :

- pour réaliser l'exo on peut poser un 'tit tableau. Dans cet exercice, on enlève 3 au nombre d'*adresses possibles* (on inclut la gateway).
  
```schema
/24 : 256 adresses possibles = 253 adresses disponibles
/25 : 128 adresses possibles = 125 adresses disponibles
/26 : 64 adresses possibles = 61 adresses disponibles
/27 : 32 adresses possibles = 29 adresses disponibles
/28 : 16 adresses possibles = 13 adresses disponibles
/29 : 8 adresses possibles = 5 adresses disponibles
```

- 57 PCs ne rentrent pas dans un `/27`, mais dans un `/26`
  - on réserve un `/26` qui permet 61 adresses IP
  - 61 adresses dispos - 57 PCs = 4 adresses restantes après affectation
- 12 serveurs ne rentrent pas dans un `/29` mais dans un `/28`
  - on réserver un `/28` qui permet 13 adresses
  - 13 adresses dispo - 12 serveurs = 1 adresse restante après affectation
- pour 26 imprimantes, on choisira un `/27`
  - 29 - 26 = 3 adresses restantes après affectation

**5.** Il existe plein de "méthodes" pour choisir ces réseaux. Pour avoir une illustration visuelle, vous pouvez vous servir de [cette app web](http://www.davidc.net/sites/default/subnets/subnets.html)

- 57 PCs, dans `10.33.0.0/26`
  - de `10.33.0.0` à `10.33.0.63`
- 26 imprimantes, dans `10.33.0.64/27`
  - de `10.33.0.64` à `10.33.0.95`
- 12 serveurs, dans `10.33.0.96/28`
  - de `10.33.0.96` à `10.33.0.111`
- ce qui nous laisse les sous-réseaux suivants libres (à l'intérieur du `/22` initial) :
  - `10.33.0.112/28`
  - `10.33.0.128/25`
  - `10.33.1.0/24`
  - `10.33.2.0/23`