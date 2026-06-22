# Dossier de Conception — Carte Acquisition de Données Vol

**Projet :** Minifusée Club Aérospatial ISEN Nantes  
**Compétition :** C'Space — CNES  
**Chef de projet :** Quentin Jallais  
**Version :** 1.2 · Mars 2026

---

## 1. Contexte et objectif

La carte embarquée doit enregistrer les données de vol (pression atmosphérique
et accélération 3 axes) depuis le décollage jusqu'à la récupération.
Les données sont stockées en mémoire flash et lues après récupération de la fusée.

---

## 2. Exigences système

| ID    | Exigence                                          | Priorité  |
|-------|---------------------------------------------------|-----------|
| EX-01 | Mesurer pression 10–1100 hPa avec résolution 1 Pa | CRITIQUE  |
| EX-02 | Mesurer accélération ±16g sur 3 axes              | CRITIQUE  |
| EX-03 | Stocker ≥ 5 min de données à 100 Hz              | HAUTE     |
| EX-04 | Alimentation 3.3 V depuis batterie LiPo 1S        | CRITIQUE  |
| EX-05 | Masse totale carte < 25 g                         | CONTRAINTE|
| EX-06 | Résistance aux vibrations décollage (> 10g)       | HAUTE     |
| EX-07 | Conformité exigences CNES C'Space v4.1            | CRITIQUE  |

---

---

## 3. Choix des composants

| Fonction       | Composant     | Justification                                      |
|----------------|---------------|----------------------------------------------------|
| Pression       | BMP388        | 1 Pa résolution, I2C, faible conso, boîtier LGA-8 |
| Accéléromètre  | LSM6DSO       | ±16g, 6 axes, FIFO intégrée, anti-aliasing         |
| MCU            | STM32F103C8   | Disponible, I2C + SPI, 72 MHz, 3.3 V              |
| Mémoire        | W25Q64 (SPI)  | 8 MB, SPI 80 MHz, faible coût, boîtier SOIC-8     |
| Régulateur     | XC6206-3.3    | LDO faible bruit, 200 mA, boîtier SOT-23          |

---

## 4. Contraintes CEM

- Plan de masse continu sur couche interne L2 (PCB 4 couches)
- Condensateurs de découplage 100 nF X7R au plus proche de chaque VCC
- Séparation des pistes analogique / numérique — zone de coupure sous BMP388
- Routage différentiel évité (signaux I2C ≤ 400 kHz — pas requis)
- Garde au sol autour du connecteur LiPo

---

## 5. Revues CNES

| Revue | Contenu                          | Statut     |
|-------|----------------------------------|------------|
| RPP   | Revue de Projet Préliminaire     | ✅ Validée |
| RPC   | Revue de Projet Critique         | ✅ Validée |
| RF    | Revue Finale avant C'Space       | ⏳ À venir |
