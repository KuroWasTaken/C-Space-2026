# 🚀 Projet Minifusée "HorizonX"

Projet de conception d'une minifusée expérimentale instrumentée pour la mesure de vitesse air et l'analyse dynamique de vol. Dans le cadre du concours C'space 2026

## 📊 Fiche Technique
| Caractéristique | Valeur |
| :--- | :--- |
| **Diamètre** | 50 mm |
| **Hauteur** | 1000 mm |
| **Masse (estimée)** | 1kg |
| **Microcontrôleur** | STM32 LO53RE |
| **Capteurs clés** | Sonde Pitot (Vitesse air), Baromètre (Altitude), IMU (Attitude) |

---

## 🛠️ Architecture du Système

### 1. Conception Mécanique (CAO)
La structure a été modélisée sous **SolidWorks**. Elle comprend une ogive aérodynamique, un tube de corps de 1m et un empennage fixe à 4 ailerons pour garantir la stabilité.



### 2. Électronique & Avionique
Le cœur du système est une carte **STM32** qui gère :
* **Mesure de vitesse :** Via une sonde Pitot et un capteur de pression différentielle.
* **Navigation :** Calcul de la trajectoire en temps réel.
* **Récupération :** Commande de l'éjecteur de parachute à l'apogée.
* <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/50da918f-cfb3-4100-b1c5-192a6c706a41" />




---

## 💻 Logiciel (Firmware)
Le code est développé en **C** via l'environnement **STM32CubeIDE**.

### Algorithme de vol :
1. **Initialisation :** Calibration des capteurs au sol.
2. **Phase de Propulsion :** Détection de l'accélération.
3. **Phase Balistique :** Lecture continue de la sonde Pitot et détection de la chute de pression (apogée).
4. **Récupération :** Activation des servomoteurs pour le parachute.

---

## 📂 Organisation du dépôt
* `/CAO` : Fichiers SolidWorks de l'assemblage et des pièces.
* `/Firmware` : Code source C et configuration .ioc.
* `/Simulations` : Courbes de stabilité et prévisions de trajectoire.

---
