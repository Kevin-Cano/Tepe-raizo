# TP4

## I. DHCP Client

🌞 **Déterminer**

- l'adresse du serveur DHCP
- l'heure exacte à laquelle vous avez obtenu votre bail DHCP
- l'heure exacte à laquelle il va expirer

```powershell
PS C:\Users\kevca> ipconfig /all

    Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
    Bail obtenu. . . . . . . . . . . . . . : lundi 13 novembre 2023 09:42:26
    Bail expirant. . . . . . . . . . . . . : mardi 14 novembre 2023 09:42:14
```

🌞 **Analyser la capture Wireshark (tcp_dhcp_client.pcapng)**

Parmi ces 4 trames, laquelle contient les informations proposées au client ?

--> Voir [ce fichier pcapng](DHCP.pcapng)

*Réponse :*  DHCP Offer

## II. Serveur DHCP

🌞 Preuve de mise en place

```powershell
[kevin@dhcp ~]$ ping pornhub.com
PING pornhub.com (66.254.114.41) 56(84) bytes of data.
    64 bytes from reflectededge.reflected.net (66.254.114.41): icmp_seq=1 ttl=53 time=15.4 ms
    64 bytes from reflectededge.reflected.net (66.254.114.41): icmp_seq=2 ttl=53 time=15.5 ms
```

```powershell
[kevin@node2 ~]$ ping hentaihaven.com
PING hentaihaven.com (188.114.97.2) 56(84) bytes of data.
    64 bytes from 188.114.97.2 (188.114.97.2): icmp_seq=1 ttl=55 time=23.0 ms
    64 bytes from 188.114.97.2 (188.114.97.2): icmp_seq=2 ttl=55 time=22.5 ms
```

```powershell
[kevin@node2 ~]$ traceroute 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
⭐ 1  _gateway (10.4.1.254)  13.708 ms  1.523 ms  1.600 ms
   2  10.0.3.2 (10.0.3.2)  2.945 ms  3.765 ms  2.965 ms
```

🌞 **Serveur DHCP**

### Installation du logiciel

```powershell
[kevin@dhcp ~]$ sudo dnf -y install dhcp-server
```

### Configuration du dhcp

```powershell
[kevin@dhcp ~]$ sudo nano /etc/dhcp/dhcpd.conf
[kevin@dhcp ~]$ sudo cat /etc/dhcp/dhcpd.conf

# Nom de domaine
option domain-name     "tp4_UwU";
# Donne un DNS
option domain-name-servers     1.1.1.1;
# Temps de bail par defaut
default-lease-time 600;
# Temps de bail max
max-lease-time 7200;
# Pour activer le serv DHCP
authoritative;
# Adresse IP du reseau et masque de sous-reseau
subnet 10.4.1.0 netmask 255.255.255.0 {
    # Il doit etre compris entre 10.4.1.137 et 10.4.1.237
    range dynamic-bootp 10.4.1.137 10.4.1.237;
    # Adresse broadcast
    option broadcast-address 10.4.1.255;
    # Passerelle
    option routers 10.4.1.254;
}

```

### Démarrage du serveur DHCP

```powershell
[kevin@dhcp ~]$ sudo systemctl enable --now dhcpd
Created symlink /etc/systemd/system/multi-user.target.wants/dhcpd.service → /usr/lib/systemd/system/dhcpd.service.

[kevin@dhcp ~]$ sudo firewall-cmd --add-service=dhcp
success

[kevin@dhcp ~]$ sudo firewall-cmd --runtime-to-permanent
success
```

### Vérification de l'état du serveur DHCP

```powershell
[kevin@dhcp ~]$ sudo systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Mon 2023-11-13 12:15:10 CET; 3min 42s ago
```

### Client DHCP

🌞 **Test !**

```powershell
#commande + rep dans powershell
```

🌞 **Prouvez que**

- node1.tp4.b1 a bien récupéré une IP dynamiquement

```powershell
[kevin@localhost ~]$ ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:b0:f1:96 brd ff:ff:ff:ff:ff:ff
    inet 10.4.1.137/24 brd 10.4.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 469sec preferred_lft 469sec
    inet6 fe80::a00:27ff:feb0:f196/64 scope link
       valid_lft forever preferred_lft forever
```

```powershell
[kevin@node1 ~]$ nmcli con show enp0s3
```

- node1.tp4.b1 a enregistré un bail DHCP
  - **déterminer la date exacte de création du bail**  
      jeudi 23 novembre 2023 15:29:48 GMT+02:00 DST
  - **déterminer la date exacte d'expiration**  
      jeudi 23 novembre 2023 15:39:48 GMT+02:00 DST
  - **déterminer l'adresse IP du serveur DHCP**  
      dhcp_server_identifier = 10.4.1.253

- Vous pouvez ping router.tp4.b1 et node2.tp4.b1 grâce à cette nouvelle IP récupérée

```powershell
[kevin@node1 ~]$ ping 10.4.1.254
PING 10.4.1.254 (10.4.1.254) 56(84) bytes of data.
64 bytes from 10.4.1.254: icmp_seq=1 ttl=64 time=1.42 ms
[kevin@node1 ~]$ ping 10.4.1.12
PING 10.4.1.12 (10.4.1.12) 56(84) bytes of data.
64 bytes from 10.4.1.12: icmp_seq=1 ttl=64 time=2.96 ms
```

🌞 **Bail DHCP serveur**

```powershell
[kevin@dhcp ~]$ cat /var/lib/dhcpd/dhcpd.leases
lease 10.4.1.137 {
  starts 4 2023/11/23 15:29:48;
  ends 4 2023/11/23 15:39:48;
  cltt 4 2023/11/23 15:29:48;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:b0:f1:96;
  uid "\001\010\000'\260\361\226";
  client-hostname "node1";
}
```

### Options DHCP

🌞 **Nouvelle conf !**

```powershell
[kevin@dhcp ~]$ sudo cat /etc/dhcp/dhcpd.conf
# Nom de domaine
option domain-name     "tp4_UwU";
# Donne un DNS
option domain-name-servers     1.1.1.1;
# Temps de bail par defaut
default-lease-time 21600;
# Temps de bail max
max-lease-time 21600;
# Pour activer le serv DHCP
authoritative;
# Adresse IP du reseau et masque de sous-reseau
subnet 10.4.1.0 netmask 255.255.255.0 {
    # Il doit etre compris entre 10.4.1.137 et 10.4.1.237
    range dynamic-bootp 10.4.1.137 10.4.1.237;
    # Adresse broadcast
    option broadcast-address 10.4.1.255;
    # Passerelle
    option routers 10.4.1.254;
}
[kevin@dhcp ~]$ sudo systemctl restart dhcpd
```

🌞 **Test !**

- vous avez enregistré l'adresse d'un serveur DNS

```powershell
[kevin@node1 ~]$ sudo cat /etc/resolv.conf
# Generated by NetworkManager
search tp4_UwU
nameserver 1.1.1.1
```

- vous avez une nouvelle route par défaut qui a été récupérée dynamiquement

```powershell
[kevin@node1 ~]$ ip r s
default via 10.4.1.254 dev enp0s3 proto dhcp src 10.4.1.137 metric 100
```

- la durée de votre bail DHCP est bien de 6 heures

```powershell
[kevin@dhcp ~]$ sudo cat /var/lib/dhcpd/dhcpd.leases
lease 10.4.1.137 {
  starts 4 2023/11/23 15:49:48; # <-- Les 6 heures
  ends 4 2023/11/23 21:49:48;
  cltt 4 2023/11/23 15:49:48;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:b0:f1:96;
  uid "\001\010\000'\260\361\226";
  client-hostname "node1";
}
```

- prouvez que vous avez un accès Internet après cet échange DHCP

```powershell
[kevin@node1 ~]$ ping pornhub.com
PING pornhub.com (66.254.114.41) 56(84) bytes of data.
64 bytes from reflectededge.reflected.net (66.254.114.41): icmp_seq=1 ttl=53 time=17.2 ms
```

🌞 Capture Wireshark

--> Voir [ce fichier pcapng](tp4_dhcp_server.pcapng)
