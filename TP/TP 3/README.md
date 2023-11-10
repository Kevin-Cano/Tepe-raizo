# TP3 : On va router des trucs

## ARP

### 1. Echange ARP

Chez marcel

```bash
[kevin@localhost ~]$ ping 10.3.1.11
PING 10.3.1.11 (10.3.1.11) 56(84) bytes of data.
64 bytes from 10.3.1.11: icmp_seq=1 ttl=64 time=1.02 ms
64 bytes from 10.3.1.11: icmp_seq=2 ttl=64 time=1.25 ms
64 bytes from 10.3.1.11: icmp_seq=3 ttl=64 time=1.57 ms
64 bytes from 10.3.1.11: icmp_seq=4 ttl=64 time=1.38 ms
```

Chez john

```bash
[kevin@localhost ~]$ ping 10.3.1.12
PING 10.3.1.12 (10.3.1.12) 56(84) bytes of data.
64 bytes from 10.3.1.12: icmp_seq=1 ttl=64 time=1.92 ms
64 bytes from 10.3.1.12: icmp_seq=2 ttl=64 time=1.03 ms
64 bytes from 10.3.1.12: icmp_seq=3 ttl=64 time=0.992 ms
64 bytes from 10.3.1.12: icmp_seq=4 ttl=64 time=0.883 ms
```

-------------------------------------------

Chez john

```bash
[kevin@localhost ~]$ ip n s
10.3.1.12 dev enp0s3 lladdr 08:00:27:c8:3f:c1 STALE
```

Chez marcel

```bash
[kevin@localhost ~]$ ip n s
10.3.1.11 dev enp0s3 lladdr 08:00:27:ba:41:1e STALE
```

- une commande pour voir la MAC de marcel dans la table ARP de john

```bash
[kevin@localhost ~]$ ip n s 10.3.1.12
10.3.1.12 dev enp0s3 lladdr ⭐08:00:27:c8:3f:c1⭐ STALE
```

- une commande pour afficher la MAC de marcel, depuis marcel

```bash
[kevin@localhost ~]$ ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether ⭐08:00:27:c8:3f:c1⭐ brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.12/24 brd 10.3.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fec8:3fc1/64 scope link
       valid_lft forever preferred_lft forever
```

### 2. Analyse de trames

🌞Analyse de trames

Vider la table ARP chez john et marcel

```bash
 sudo ip neigh flush all
```

Chez john, capture de trame

```bash
[kevin@localhost ~]$ sudo tcpdump -i enp0s3 -c 20 -w tp3_arp.pcapng not port 22
```

Chez marcel, ping john

```bash
[kevin@localhost ~]$ ping 10.3.1.11
```

## II. Routage

- Commande pour ajouter les routes statiques :
  - Pour john :

```bash
[kevin@localhost ~]$ sudo nano /etc/sysconfig/network-scripts/route-enp0s3 
```

```bash
[kevin@localhost ~]$ sudo cat /etc/sysconfig/network-scripts/route-enp0s3
10.3.2.0/24 via 10.3.1.254 dev enp0s3
[kevin@localhost ~]$ sudo systemctl restart NetworkManager
```

- Pour marcel :

```bash
[kevin@localhost ~]$ sudo nano /etc/sysconfig/network-scripts/route-enp0s3
```

```bash
[kevin@localhost ~]$ sudo cat /etc/sysconfig/network-scripts/route-enp0s3
10.3.1.0/24 via 10.3.2.254 dev enp0s3
[kevin@localhost ~]$ sudo systemctl restart NetworkManager
```

### Analyse de trames

```bash
#commandes chez routeur, marcel et john 
```

🌞Analyse des échanges ARP

| ordre | type trame  | IP source           | MAC source                   | IP destination      | MAC destination              |
| ----- | ----------- | ------------------- | ---------------------------- | ------------------- | ---------------------------- |
| 1     | ???         | ???                 | ???                          | ???                 | ???                          |
| 2     | ???         | ???                 | ???                          | ???                 | ???                          |
| 3     | ???         | ???                 | ???                          | ???                 | ???                          |
| 3     | ???         | ???                 | ???                          | ???                 | ???                          |
| 4     | ???         | ???                 | ???                          | ???                 | ???                          |
| 5     | ???         | ???                 | ???                          | ???                 | ???                          |
| 6     | ???         | ???                 | ???                          | ???                 | ???                          |
| 6     | ???         | ???                 | ???                          | ???                 | ???                          |

### Accès internet

🌞 **Donnez un accès internet à vos machines - config routeur**

Vérification de l'accès à Internet (depuis routeur) :

```powershell
#commande + rep dans powershell
```

Autoriser le routage des paquets sur internet :

```powershell
#commande + rep dans powershell
```

Ajouter une route par defaut :

```powershell
#commande + rep dans powershell
```

🌞 **Donnez un accès internet à vos machines - config clients**

```powershell
#commandes + rep dans powershell
```

Vérification de l'accès à Internet (depuis marcel et john) :

```powershell
#commandes + rep dans powershell
```

🌞Analyse de trames

| ordre | type trame  | IP source           | MAC source                   | IP destination      | MAC destination              |
| ----- | ----------- | ------------------- | ---------------------------- | ------------------- | ---------------------------- |
| 1     | ???         | ???                 | ???                          | ???                 | ???                          |
| 2     | ???         | ???                 | ???                          | ???                 | ???                          |
| 3     | ???         | ???                 | ???                          | ???                 | ???                          |
| 4     | ???         | ???                 | ???                          | ???                 | ???                          |
