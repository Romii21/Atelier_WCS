# Atelier_DHCP_avec_Debian

Configuration complète d'un serveur DHCP sur Debian avec étendue et réservation d'adresse.

## Configuration :

* Réseau : 172.20.0.0/24
* Serveur DHCP : 172.20.0.1
* Étendue DHCP : 172.20.0.80 - 172.20.0.150
* Réservation : 172.20.0.100 (Debian)

## Serveur DHCP (Windows Serveur) :

Configuration du serveur DHCP :

* Dans le fichier /etc/network/interfaces  
![Serveur_IP](Ressources/DHCP_Debian_Serveur/Serveur_IP.PNG)

* Dans le fichier /etc/dhcp/dhcp.conf  
![Serveur_DHCP_config](Ressources/DHCP_Debian_Serveur/Serveur_DHCP_config.PNG)

## Client (Ubuntu) :

Configuration IP du Client 1 :

* En interface graphique

| ![Ubuntu_IP](Ressources/DHCP_Debian_Serveur/Ubuntu_IP.PNG) | ![Ubuntu_IP_2](Ressources/DHCP_Debian_Serveur/Ubuntu_IP_2.PNG) |
| --------------------------- | ------------------------------- |

## Client 2 (Windows 11) :

Configuration IP du Client 2 :

* Dans le fichier /etc/dhcp/dhcp.conf du serveur Debian  
![Debian_DHCP_config_2](Ressources/DHCP_Debian_Serveur/Debian_DHCP_config_2.PNG)

* Sur le client 2  
![Windows_IP](Ressources/DHCP_Debian_Serveur/Windows_IP.PNG)
