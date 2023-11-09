# TP 5

## I. First steps

🌞 Déterminez, pour ces 5 applications, si c'est du TCP ou de l'UDP

- Discord UDP  
ip local: 10.33.70.251, port local: 59419  
ip server: 66.22.197.57, port server: 50017  
- Osu TCP  
ip local: 10.33.70.251, port local: 51989  
ip server: 172.67.14.100, port server: 443  
- Youtube UDP  
ip local: 10.33.70.251, prot local: 58343  
ip server: 91.68.245.15, port server: 443  
- Hollow Knight TCP  
ip local: 10.33.70.251, port local: 52210  
ip server: 20.109.157.180, port server: 443  
- League Of Legends UDP  
ip local: 10.33.70.251, port local: 54503   
ip server: 162.249.78.58, port server: 5364  

🌞 Demandez l'avis à votre OS
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

🌞 Examinez le trafic dans Wireshark
