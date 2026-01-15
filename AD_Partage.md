# AD_Partage

Dans cet exercice l'objectif est de créer un dossier partagé sur un serveur Windows 2022, pour que chaque utilisateurs du domaine puisse acceder au dossier qui le concerne.
La documentation qui suit permet de suivre pas à pas les étapes pour créer, configurer et tester le dossier partagé.
  
## 1. Serveur AD

### Création et configuration de l'Active Directory :
  - Domaine : lab.lan
  - OU : LabSecurity - LabComputers - LabUsers

### Création des utilisateurs et des groupes qui composeront le domaine : 
  - Users :
    - Direction
    - Comptabilité
    - RH
    - Wilder
  
  - Groupes :
    - GrpUsersDirection
    - GrpUsersComptabilité
    - GrpUsersRH

Pensez à bien mettre les utilisateurs et les groupes dans les OU correspondantes.

| Utilisateurs | Groupes |
| ------------ | ------- |
| ![Ressources/AD_Partage/serveur_users](Ressources/AD_Partage/serveur_users.png) | ![Ressources/AD_Partage/serveur_groupes](Ressources/AD_Partage/serveur_groupes.png) |

---

## 2. Dossier Partagé

### Création du dossier partagé sur la racine du serveur :
  - Nom : Documents_Entreprise
  - Emplacement : C:\

L'action peut s'effectuer des deux manières suivantes.

| CLI | GUI |
| --- | --- |
| ![Ressources/AD_Partage/serveur_dossier_partage_crea](Ressources/AD_Partage/serveur_dossier_partage_crea.png) | ![Ressources/AD_Partage/serveur_dossier_partage_crea_2](Ressources/AD_Partage/serveur_dossier_partage_crea_2.png) |

### Création des sous-dossiers :
  - Nom :
    - Direction
    - Comptabilité
    - RH
  - Emplacement : C:\Dossiers_Entreprise

L'action peut s'effectuer des deux manières suivantes.

| CLI | GUI |
| --- | --- |
| ![Ressources/AD_Partage/serveur_dossier_partage_crea_4](Ressources/AD_Partage/serveur_dossier_partage_crea_4.png) | ![Ressources/AD_Partage/serveur_dossier_partage_crea_3](Ressources/AD_Partage/serveur_dossier_partage_crea_3.png) |

### Initialisatiion du partage du "Dossiers_Entreprise" :
  - Nom : Docs
  - Emplacement : C:\Dossiers_Entreprise
  - Tout les droits : Administators
  - Droit de lecture : Domain Users

Avec les détails ci-dessus cette commande montre comment partagé le dossier avec des règles bien précisent.

![Ressources/AD_Partage/serveur_dossier_partage_config](Ressources/AD_Partage/serveur_dossier_partage_config.png)

---

## 3. Droits et partage des sous-dossiers

### Sous-dossier Direction :
  - Droits de lecture :
    - Direction
  - Droits d'écriture :
    - Direction

Pensez bien à désactiver l'héritage dans les paramètres avancés de sécurité.

![Ressources/AD_Partage/serveur_dossier_partage_direction_droits_3](Ressources/AD_Partage/serveur_dossier_partage_direction_droits_3.png)

Le sous-dossier direction n'est accessible que par le Groupe Direction (GrpUsersDirection).  
L'action s'effectue dans les propriétés du dossier dans l'onglet sécurité, vous devez ajouter le groupe correspondant aux dossier et mettre droit de lecture et d'écriture.

![Ressources/AD_Partage/serveur_dossier_partage_direction_droits](Ressources/AD_Partage/serveur_dossier_partage_direction_droits.png)

### Sous-dossier Comptabilité :
  - Droits de lecture :
    - Direction
    - Comptabilité
  - Droits d'écriture :
    - Direction
    - Comptabilité

Pensez bien à désactiver l'héritage dans les paramètres avancés de sécurité.

![Ressources/AD_Partage/serveur_dossier_partage_compta_droits_3](Ressources/AD_Partage/serveur_dossier_partage_compta_droits_3.png)

Le sous-dossier comptabilité est accessible que par le Groupe Compabilité et le Groupe Direction (GrpUsersComptabilite - GrpUsersDirection).  
L'action s'effectue dans les propriétés du dossier dans l'onglet sécurité, vous devez ajouter le groupe correspondant aux dossier et mettre droit de lecture et d'écriture.

| ![Ressources/AD_Partage/serveur_dossier_partage_compta_droits_2](Ressources/AD_Partage/serveur_dossier_partage_compta_droits_2.png) | ![Ressources/AD_Partage/serveur_dossier_partage_compta_droits.png](Ressources/AD_Partage/serveur_dossier_partage_compta_droits.png) |
| --- | --- |

---
### Sous-dossier RH :
  - Droits de lecture :
    - Direction
    - RH
  - Droits d'écriture :
    - Direction
    - RH

Pensez bien à désactiver l'héritage dans les paramètres avancés de sécurité.

![Ressources/AD_Partage/serveur_dossier_partage_RH_droits_3](Ressources/AD_Partage/serveur_dossier_partage_RH_droits_3.png)

Le sous-dossier RH est accessible que par le Groupe RH et le Groupe Direction (GrpUsersRH - GrpUsersDirection).  
L'action s'effectue dans les propriétés du dossier dans l'onglet sécurité, vous devez ajouter le groupe correspondant aux dossier et mettre droit de lecture et d'écriture.

| ![Ressources/AD_Partage/serveur_dossier_partage_RH_droits_2](Ressources/AD_Partage/serveur_dossier_partage_RH_droits_2.png) | ![Ressources/AD_Partage/serveur_dossier_partage_RH_droits.png](Ressources/AD_Partage/serveur_dossier_partage_RH_droits.png) |
| --- | --- |

---

## 4. Test machine Client

Une fois le client lié au domaine du serveur AD vous pourrez tester les accès de chaque utilisteurs sur les dossiers.

### Utilisteur Direction

Initialisation du partage via CLI.  
Le dossier partagé se retrouve sur le disque "Z" du client.

![Ressources/AD_Partage/client_direction_dossier_partage](Ressources/AD_Partage/client_direction_dossier_partage.png)

Test du partage via CLI.  
Vous pouvez observez que l'utilisateur "Direction" à accès à tout les dossiers.

![Ressources/AD_Partage/client_direction_dossier_partage_test](Ressources/AD_Partage/client_direction_dossier_partage_test.png)

### Utilisteur Comptabilité

Initialisation du partage via CLI.  
Le dossier partagé se retrouve sur le disque "Z" du client.

![Ressources/AD_Partage/client_compta_dossier_partage](Ressources/AD_Partage/client_compta_dossier_partage.png)

Test du partage via CLI.  
Vous pouvez observez que l'utilisateur "Comptabilité" n'à accès que à son dossier.

![Ressources/AD_Partage/client_compta_dossier_partage_test](Ressources/AD_Partage/client_compta_dossier_partage_test.png)

### Utilisteur RH

Initialisation du partage via CLI.  
Le dossier partagé se retrouve sur le disque "Z" du client.

![Ressources/AD_Partage/client_RH_dossier_partage](Ressources/AD_Partage/client_RH_dossier_partage.png)

Test du partage via CLI.  
Vous pouvez observez que l'utilisateur "RH" n'à accès que à son dossier.

![Ressources/AD_Partage/client_RH_dossier_partage_test](Ressources/AD_Partage/client_RH_dossier_partage_test.png)

### Utilisteur Wilder

Initialisation du partage via CLI.  
Le dossier partagé se retrouve sur le disque "Z" du client.

![Ressources/AD_Partage/client_wilder_dossier_partage](Ressources/AD_Partage/client_wilder_dossier_partage.png)

Test du partage via CLI.  
Vous pouvez observez que l'utilisateur "Wilder" n'à accès à aucun dossier.

![Ressources/AD_Partage/client_wilder_dossier_partage_test](Ressources/AD_Partage/client_wilder_dossier_partage_test.png)

---
