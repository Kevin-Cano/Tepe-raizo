# TP 1

## I. Exploration locale en solo

### 1. Affichage d'informations sur la pile TCP/IP locale

🌞 **Affichez les infos des cartes réseau de votre PC**

```powershell
PS C:\Users\kevca> ipconfig
```

**Réponse :**

```powershell
Carte Ethernet Ethernet 2 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::1b90:386f:5e0a:13d4%22
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

Carte Ethernet Ethernet 3 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::a055:72f4:929c:e71b%13
   Adresse IPv4. . . . . . . . . . . . . .: 10.3.1.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

Carte Ethernet Ethernet 4 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::532a:a0bf:8098:13cf%61
   Adresse IPv4. . . . . . . . . . . . . .: 10.5.1.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

Carte réseau sans fil Connexion au réseau local* 1 :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte réseau sans fil Connexion au réseau local* 2 :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::f3d7:ae78:d6dd:2e68%3
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.70.251
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```

🌞 **Affichez votre gateway**

```powershell
PS C:\Users\kevca> ipconfig
```

**Réponse :**

```powershell
Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::f3d7:ae78:d6dd:2e68%3
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.70.251
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```

🌞 **Déterminer la MAC de la passerelle**

```powershell
PS C:\Users\kevca> arp -a
```

**Réponse :**

```powershell
Interface : 10.33.70.251 --- 0x3
  Adresse Internet      Adresse physique      Type
  10.33.67.208          54-14-f3-ab-c9-21     dynamique
  10.33.70.110          ac-74-b1-21-c4-b5     dynamique
  10.33.70.190          98-8d-46-c4-fa-e5     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique⭐
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

🌞 **Trouvez comment afficher les informations sur une carte IP**

Panneau de config > Réseau et internet > Centre de réseau et partage > Wi-Fi@YNOV > Détails

```bash
    Adresse physique: 10-B1-DF-75-D5-2F
    Adresse IPv4: 10.33.70.251
    Passerelle par défaut IPv4: 10.33.79.254
```

### 2. Modifications des informations

#### A. Modification d'adresse IP (part 1)

**🌞 Utilisez l'interface graphique de votre OS pour changer d'adresse IP :**

Pramaètres > Réseau et internet > Param réseau avancés > Wifi > Afficher les propriétés supplémentaires > Modifier

**🌞 Il est possible que vous perdiez l'accès internet.** Que ce soit le cas ou non, expliquez pourquoi c'est possible de perdre son accès internet en faisant cette opération.

**Réponse :** Parce que l'adresse IP que j'ai choisi est probablement déjà utilisée par un autre utilisateur de mon réseau.

## II. Exploration locale en duo

### Modification d'adresse IP

**🌞 Modification de nos adresses IP en utilisant le GUI (windows)**  
Adresse IP choisies :   t'as choisi quoi fdp
  
🌞 **Vérifier à l'aide d'une commande que votre IP a bien été changée**

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans powershell
```

🌞 **Vérifier que les deux machines se joignent**

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans powershell
```

🌞 **Déterminer l'adresse MAC de votre correspondant**

```powershell
#commande
```

**Réponse :**
```powershell
#réponse dans powershell
```

### Petit chat privé 🐱

🌞 **sur le PC serveur**

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans powershell
```

🌞 **sur le PC client**

```powershell
#commande
```

**Réponse :**
*ça fé quoa (tu verra c joli on peut envoyé des UWU à son coéquipier)

🌞 **Visualiser la connexion en cours**

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans le powershell
```

**🌞 Pour aller un peu plus loin**

```powershell
#commande
```

**Réponse :**  

```powershell
#réponse dans powershell
```

## Firewall

🌞 **Activez et configurez votre firewall**

- **Autoriser le ping**

- **Autoriser le traffic sur le port qu'utilise nc**

## Utilisation d'un des deux comme gateway

**🌞Tester l'accès internet depuis le PC client**

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans powershell
```

**🌞 Prouver que la connexion Internet passe bien par l'autre PC**

```powershell
#commande
``` 

**Réponse :**

```powershell
#réponse dans le powershell
``` 

## III. Manipulations d'autres outils/protocoles côté client

### 1. DHCP

**🌞Exploration du DHCP, depuis votre PC**

```powershell
#commande
```

**Reponse :**

```powershell
#réponse dans le powershell
```

### 2. DNS

🌞**Trouver l'adresse IP du serveur DNS que connaît votre ordinateur**

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans le powershell
```

**🌞 Utiliser, en ligne de commande l'outil nslookup**

- **Un lookup pour google.com**

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans powershell
```

- **Puis pour Ynov :** 

```powershell
#commande
```

**Réponse :**

```powershell
#réponse dans powershell
```

L'adresse IP du serveur à qui on vient d'effectuer ces requêtes est 8.8.8.8

- **Un lookup pour l'adresse : 231.34.113.12**

```powershell
#commande
```

**Reponse :**

```powershell
#réponse dans powershell
```

- **Un lookup pour l'adresse : 231.34.113.12**

```powershell
#commande
```

**Reponse :**

```powershell
#réponse dans le powershell
```

## IV. Wireshark

**🌞 Utilisez le pour observer les trames qui circulent entre vos deux carte Ethernet. Mettez en évidence :**

- **un ping entre vous et votre mate**

```powershell
#commande
```

**Réponse :**
--> capture écran wireshark attendue

- **un ping entre vous et la passerelle du réseau**

```powershell
#commande
```

**Réponse :**
--> capture écran wireshark attendue

- **un netcat entre vous et votre mate, branché en RJ45**

```powershell
#commande
```

**Réponse :**
--> capture écran wireshark attendue

- **Identifiez dans la capture le serveur DNS à qui vous posez la question.**

```powershell
#commande
```

**Réponse :**
--> capture écran wireshark attendue  
à qui t'as posé la question : ???
