# TP2 : Ethernet, IP, et ARP

# Sommaire

- [TP2 : Ethernet, IP, et ARP](#tp2--ethernet-ip-et-arp)
- [Sommaire](#sommaire)
- [0. Prérequis](#0-prérequis)
- [I. Setup IP](#i-setup-ip)
- [II. ARP my bro](#ii-arp-my-bro)
- [II.5 Interlude hackerzz](#ii5-interlude-hackerzz)
- [III. DHCP you too my brooo](#iii-dhcp-you-too-my-brooo)




# I. Setup IP

🌞 **Mettez en place une configuration réseau fonctionnelle entre les deux machines**

`Netsh interface ip set address "Ethernet" static 10.10.10.70 255.255.252.0`

```
Adresse IPv4. . . . . . . . . . . . . .: 10.10.10.70
   Masque de sous-réseau. . . . . . . . . : 255.255.252.0
   Adresse Reseau           = 10.10.8.0
  - l'adresse de broadcast  = 10.10.11.255
```



🌞 **Prouvez que la connexion est fonctionnelle entre les deux machines**
```
 ping 10.10.10.69
Envoi d’une requête 'Ping'  10.10.10.69 avec 32 octets de données :
Réponse de 10.10.10.69 : octets=32 temps=1 ms TTL=64
Réponse de 10.10.10.69 : octets=32 temps<1ms TTL=64
Réponse de 10.10.10.69 : octets=32 temps=1 ms TTL=64
Réponse de 10.10.10.69 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.10.10.69:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 1ms, Moyenne = 0ms
```

🌞 **Wireshark it**


# II. ARP my bro

ARP permet, pour rappel, de résoudre la situation suivante :

- pour communiquer avec quelqu'un dans un LAN, il **FAUT** connaître son adresse MAC
- on admet un PC1 et un PC2 dans le même LAN :
  - PC1 veut joindre PC2
  - PC1 et PC2 ont une IP correctement définie
  - PC1 a besoin de connaître la MAC de PC2 pour lui envoyer des messages
  - **dans cette situation, PC1 va utilise le protocole ARP pour connaître la MAC de PC2**
  - une fois que PC1 connaît la mac de PC2, il l'enregistre dans sa **table ARP**

🌞 **Check the ARP table**

-  arp -a
```
Adresse Internet      Adresse physique      Type
  10.10.10.69           5c-60-ba-75-5c-83     dynamique
```
- Adresse physique 5c-60-ba-75-5c-83

  - ```
10.33.19.254
```


🌞 **Manipuler la table ARP**
arp -d ; arp -a
```
Interface : 10.10.10.70 --- 0x8
  Adresse Internet      Adresse physique      Type
  224.0.0.22            01-00-5e-00-00-16     statique

Interface : 192.168.174.1 --- 0x11
  Adresse Internet      Adresse physique      Type
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.252           01-00-5e-00-00-fc     statique

Interface : 192.168.88.1 --- 0x15
  Adresse Internet      Adresse physique      Type
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.252           01-00-5e-00-00-fc     statique

Interface : 10.33.16.222 --- 0x16
  Adresse Internet      Adresse physique      Type
  10.33.19.254          00-c0-e7-e0-04-4e     dynamique
  224.0.0.22            01-00-5e-00-00-16     statique
```
🌞 **Wireshark it**
