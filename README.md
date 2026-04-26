# 🔐 Android Rooting & Security Analysis Lab

## 📌 Introduction

Ce laboratoire a pour objectif de comprendre le fonctionnement du **rooting Android** ainsi que son impact sur la sécurité des applications.
L’expérimentation a été réalisée dans un environnement contrôlé à l’aide d’un émulateur Android (AVD).

---

## 🎯 Objectifs

* Comprendre le concept de **rooting**
* Analyser les impacts sur la sécurité Android
* Tester une application dans un environnement rooté
* Identifier les risques et proposer des mesures de sécurité

---

## 📍 Périmètre du test

* **Application :** Application Android de gestion des étudiants
* **Support :** Android Virtual Device (AVD)
* **Objectif :** Analyse des impacts du rooting
* **Données :** Fictives
* **Réseau :** Environnement de test local

---

## ⚙️ Environnement

* Android Studio
* AVD (Pixel 5 API 35)
* ADB (Android Debug Bridge)
* Backend : PHP + MySQL (XAMPP)

---

## 🧪 Scénarios de test

1. Lancement de l’application
2. Ajout d’un étudiant
3. Consultation

https://github.com/user-attachments/assets/efa31e1d-2afd-42d9-adb6-541725d9bcbd



---

## 🔓 Rooting de l’AVD

### Commandes utilisées

```
adb root
adb remount
adb shell id
```

### Résultat

* Accès root obtenu (`uid=0(root)`)
* Contrôle total du système

📸 **Capture : adb root / adb shell id**
<img width="1918" height="388" alt="snap3 root" src="https://github.com/user-attachments/assets/ad282b81-4f70-4acc-9312-f34ed65c7203" />

---

## 🔐 Sécurité Android

### Verified Boot

Verified Boot garantit l’intégrité du système au démarrage en vérifiant les signatures.

### AVB (Android Verified Boot)

AVB améliore Verified Boot en ajoutant :

* vérification avancée des partitions
* protection contre le rollback

---

##  Définition du Root

Le rooting permet d’obtenir les privilèges super-utilisateur sur Android.
Il donne un accès complet au système et permet de modifier des éléments protégés.
Il est utile en laboratoire pour l’analyse de sécurité.
Cependant, il représente un risque important en production.

---

## 📂 Analyse des données

Accès au répertoire :

```bash
/data/data/com.example.projetws
```

### Résultat :

* Aucun fichier sensible trouvé
* Dossiers présents : `files`, `cache`, `code_cache`

📸 **Capture : accès au dossier /data/data**
<img width="1871" height="680" alt="snap4 ls" src="https://github.com/user-attachments/assets/da2c9c6f-27b1-496d-a397-612f05107590" />
<img width="987" height="111" alt="snap 5 ls data" src="https://github.com/user-attachments/assets/a8305175-c1a8-47be-a624-1645f0f8b12c" />
<img width="923" height="352" alt="snap5 ls data 2" src="https://github.com/user-attachments/assets/5225a8bd-dfbb-48f4-8073-76ddaecc4b69" />

---

## 🌐 Analyse réseau

L’application communique avec un serveur MySQL via API PHP.

### Risques identifiés :

* Utilisation potentielle de HTTP (non sécurisé)
* Absence d’authentification
* API accessible publiquement

---

## ⚠️ Matrice des risques

* Intégrité du système compromise après root
* Accès non autorisé aux données
* Fuite d’informations via logs
* Communication réseau non sécurisée
* API exposée sans protection
* Instabilité du système
* Absence de contrôle d’accès
* Traçabilité insuffisante

---

## 🛡️ Mesures défensives

* Utilisation de HTTPS
* Mise en place d’authentification
* Chiffrement des données sensibles
* Isolation du réseau
* Suppression des logs sensibles
* Validation des entrées (anti-SQL injection)
* Utilisation d’un environnement de test
* Réinitialisation après test

---

## 📊 OWASP MASVS

* **STORAGE-1 :** Stockage sécurisé des données sensibles
* **NETWORK-1 :** Utilisation de TLS pour les communications

---

## 🧪 OWASP MASTG

* Analyse des fichiers dans `/data/data`
* Surveillance des logs avec `adb logcat`

---

## 🔄 Remise à zéro

L’AVD a été réinitialisé après les tests via :

* Android Studio → Device Manager → Wipe Data

<img width="782" height="856" alt="Screenshot 2026-04-26 210701" src="https://github.com/user-attachments/assets/77adb5b2-e929-4f26-843c-3adb77636e79" />

📸 **Capture : écran initial Android**
<img width="792" height="761" alt="Screenshot 2026-04-26 210833" src="https://github.com/user-attachments/assets/bb983c5a-aacc-4f2f-ada1-7a56bda78452" />


---

## ✅ Conclusion

Le rooting permet d’obtenir un accès complet au système Android et de contourner les mécanismes de sécurité.
L’analyse a montré que l’application ne stocke pas de données sensibles localement.
Cependant, les risques principaux se situent au niveau du réseau et de l’API backend.
Il est donc essentiel de sécuriser les communications et de protéger les accès aux services.

---

## 📌 Auteur

* Nom : ASSEKNOUR Sana
* École : ENSA Marrakech
* Filière : Génie Cyberdéfense et Systèmes de Télécommunications
