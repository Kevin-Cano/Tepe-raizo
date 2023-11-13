# TP 5

## I. First steps

🌞 **Déterminez, pour ces 5 applications, si c'est du TCP ou de l'UDP**

- **Discord** UDP  
ip local: 10.33.70.251, port local: 62608  
ip server: 66.22.197.143, port server: 50006  

--> Voir [ce fichier pcapng](tp5_trame1.pcapng)

- **Osu** TCP  
ip local: 10.33.70.251, port local: 7680  
ip server: 10.33.73.120, port server: 52965  

--> Voir [ce fichier pcapng](tp5_trame2.pcapng)

- **Youtube** UDP  
ip local: 10.33.70.251, prot local: 64541  
ip server: 77.136.192.81, port server: 443  

--> Voir [ce fichier pcapng](tp5_trame3.pcapng)

- **Hollow Knight** TCP  
ip local: 10.33.70.251, port local: 51291  
ip server: 162.247.241.2, port server: 443  

--> Voir [ce fichier pcapng](tp5_trame4.pcapng)

- **League Of Legends** UDP  
ip local: 10.33.70.251, port local: 51791   
ip server: 162.249.78.45, port server: 5151  

--> Voir [ce fichier pcapng](tp5_trame5.pcapng)

🌞 **Demandez l'avis à votre OS**
```powershell
PS C:\Windows\system32> netstat

Connexions actives

  Proto  Adresse locale         Adresse distante            État

  # Discord
  UDP    10.33.70.251:59419     66.22.197.57:50017          ESTABLISHED
  # Osu
  UDP    10.33.70.251:51989     172.67.14.100:https         ESTABLISHED
  # Youtube
  TCP    10.33.70.251:58343     91.68.245.15:https          ESTABLISHED
  # Hollow Knight
  UDP    10.33.70.251:52210     20.109.157.180:https        ESTABLISHED
  # League Of Legends
  UDP    10.33.70.251:54503     162.249.78.58:5364          ESTABLISHED
  ```

## II. Setup Virtuel
### 1. SSH

🌞 **Examinez le trafic dans Wireshark**

- Déterminez si SSH utilise TCP ou UDP

⭐ SSH utilise TCP

- Repérez le 3-Way Handshake à l'établissement de la connexion
- Repérez du trafic SSH
- Repérez le FIN ACK à la fin d'une connexion

--> Voir [ce fichier pcapng](tp5_3_way.pcapng)

🌞 **Demandez aux OS**

- Repérez, avec une commande adaptée (netstat ou ss), la connexion SSH depuis votre machine

```powershell
PS C:\Users\kevca> netstat

Connexions actives

  Proto  Adresse locale         Adresse distante       État
  TCP    10.5.1.1:65232         10.5.1.11:ssh          ESTABLISHED
```

- ET repérez la connexion SSH depuis la VM

```powershell
[kevin@node1 ~]$ ss -t
State        Recv-Q        Send-Q               Local Address:Port               Peer Address:Port        Process
ESTAB        0             52                       10.5.1.11:ssh                    10.5.1.1:65232
```

### 2. Routage

🌞 **Prouvez que**

- node1.tp5.b1 a un accès internet
```powershell
[kevin@node1 ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=112 time=33.0 ms
```

- node1.tp5.b1 peut résoudre des noms de domaine publics (comme ynov.com)
```powershell
[kevin@node1 ~]$ ping jacquieetmichel.net
PING jacquieetmichel.net (104.19.142.72) 56(84) bytes of data.
64 bytes from 104.19.142.72 (104.19.142.72): icmp_seq=1 ttl=55 time=24.0 ms
64 bytes from 104.19.142.72 (104.19.142.72): icmp_seq=2 ttl=55 time=23.0 ms
64 bytes from 104.19.142.72 (104.19.142.72): icmp_seq=3 ttl=55 time=23.5 ms
64 bytes from 104.19.142.72: icmp_seq=4 ttl=55 time=23.3 ms

--- jacquieetmichel.net ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 15208ms
```

### 3. Serveur WEB  

🌞 **Installez le paquet nginx**  

```powershell
[kevin@web ~]$ sudo dnf install nginx -y
```

🌞 **Créer le site web**  

```powershell
[kevin@web var]$ sudo mkdir www
[kevin@web www]$ sudo mkdir site_web_nul
[kevin@web site_web_nul]$ sudo nano index.html

#Dans index.html j'ai mis <h1>MEOW</h1>
```

🌞 **Donner les bonnes permissions**

```powershell
[kevin@web ~]$ sudo chown -R nginx:nginx /var/www/site_web_nul
```

🌞 **Créer un fichier de configuration NGINX pour notre site web**

```powershell
[kevin@web ~]$ sudo nano /etc/nginx/conf.d/site_web_nul.conf
```

🌞 **Démarrer le serveur web !**

```powershell
[kevin@web ~]$ sudo systemctl start nginx
[kevin@web ~]$ systemctl status nginx
```

🌞 **Ouvrir le port firewall**

```powershell
[kevin@web ~]$ sudo firewall-cmd --add-port=80/tcp --permanent
[kevin@web ~]$ sudo firewall-cmd --reload
```

🌞 **Visitez le serveur web !**

```powershell
[kevin@node1 ~]$ curl http://10.5.1.12
<h1>MEOW</h1>
```

🌞 **Visualiser le port en écoute**

```powershell
[kevin@web ~]$ ss -a -t -n -l
State         Recv-Q        Send-Q               Local Address:Port               Peer Address:Port       Process
LISTEN        0             511                        0.0.0.0:80                      0.0.0.0:*
```

🌞 **Analyse trafic**

```powershell
[kevin@web ~]$ sudo tcpdump -i enp0s3 -w tp5_web.pcapng not port 22
```
--> Voir [ce fichier pcapng](tp5_web.pcapng)
