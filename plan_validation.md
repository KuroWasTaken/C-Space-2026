# Plan de Validation — Système Électronique Embarqué

**Projet :** Carte acquisition vol Minifusée  
**Référence :** CNES C'Space v4.1 — Section 5.3  
**Version :** 1.1

---

## Niveau 1 — Test composant (post-soudure)

| Test | Méthode | Critère |
|------|---------|---------|
| Continuité | Multimètre — toutes les pistes critiques | Résistance < 1 Ω |
| Court-circuit | Multimètre entre VCC et GND | Résistance > 10 kΩ hors charge |
| Tension 3.3 V | Multimètre sur test-point TP1 | 3.28 – 3.32 V |

---

## Niveau 2 — Test module

| Module | Test | Critère |
|--------|------|---------|
| BMP388 | Lecture pression ambiante via I2C | 1013 ± 20 hPa |
| LSM6DSO | Accélération repos axe Z | 1.00 ± 0.05 g |
| Flash W25Q64 | Écriture + relecture 1 Mo | Données identiques (CRC32) |
| UART debug | Transmission à 115200 bauds | Pas de frame error |

---

## Niveau 3 — Test système

### 3.1 Acquisition complète
- Démarrer l'enregistrement
- Secouer la carte pendant 60 secondes
- Récupérer les données Flash
- Vérifier la cohérence temporelle (pas de trou, pas de doublon)

**Critère :** 100 % des trames enregistrées, horodatage cohérent

### 3.2 Test vibrations simulées
- Fixer la carte sur pot vibrant (ou perceuse + support)
- Vibrations 20–200 Hz, amplitude 5g, durée 30 s
- Vérifier absence de reset MCU et de corruption Flash

**Critère :** Aucun reset · Données lisibles après vibrations

### 3.3 Test autonomie batterie
- LiPo 1S 500 mAh
- Enregistrement continu jusqu'à coupure LDO

**Critère :** Autonomie ≥ 8 minutes

---

## Résultats

| Test        | Résultat     | Conforme |
|-------------|--------------|----------|
| Continuité  | OK toutes pistes | ✅ |
| Tension 3.3V | 3.30 V mesurée | ✅ |
| BMP388      | 1011 hPa     | ✅       |
| LSM6DSO     | 0.98 g axe Z | ✅       |
| Flash CRC   | CRC identique | ✅      |
| Vibrations  | 0 reset · données OK | ✅ |
| Autonomie   | 9 min 42 s   | ✅       |

**Statut global : ✅ VALIDÉ — Prêt pour revue CNES RPC**
