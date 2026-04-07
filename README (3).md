# 🎯 Laser Run EPS

> Application web progressive dédiée à l'évaluation du **Laser Run** en cours d'Éducation Physique et Sportive (EPS).  
> Conçue pour une utilisation en temps réel sur le terrain, depuis un smartphone.

---

## 📋 Description

**Laser Run EPS** est une application web mono-fichier (`index.html`) permettant à un enseignant d'EPS de gérer et d'évaluer des séances de Laser Run en milieu scolaire.  
Les élèves utilisent l'application sur leur propre téléphone pour saisir leurs données de passage, qui sont synchronisées en temps réel vers l'espace enseignant via Firebase.

---

## 🎯 Contexte et objectif

Le Laser Run est une activité combinant course à pied et tir laser sur cible. Ce projet répond au besoin d'automatiser :

- La **saisie des données** de chaque passage élève (chronomètre, tirs, LEDs atteintes)
- Le **calcul automatique de la note** sur 20 selon un barème officiel
- Le **suivi en temps réel** par l'enseignant depuis un second appareil
- L'**archivage des résultats** de la séance

---

## ✨ Aperçu des fonctionnalités

### 🎯 Espace Élève — Page Passage

| Fonctionnalité | Description |
|---|---|
| Saisie des informations | Nom, prénom, sexe, parcours, distance de tir, numéro de piste, temps projet |
| Session obligatoire | Code de session requis avant tout passage (modal plein écran) |
| Chronomètre général | Démarrage/pause/reset du temps total Laser Run |
| 3 passages de tir | Chronomètre individuel, compteur de tirs (+/−), LEDs allumées (clic direct) |
| Mode 1 main / 2 mains | Bonus +0.5 pt par passage validé à 1 main |
| Bouton 🏁 Arrivée | Arrêt du chrono après la dernière course (séquence correcte) |
| Calcul automatique | Note /20 calculée à la fin (tir, course, projet, difficulté) |
| Synchronisation Firebase | Résultat envoyé chiffré vers la session enseignant |

### 👨‍🏫 Espace Enseignant — Accès sécurisé

| Onglet | Fonctionnalités |
|---|---|
| 🟢 Présence | Élèves connectés en temps réel, triés par numéro de couloir, pénalités en direct |
| 📋 Résultats | Tableau complet des passages, modification du parcours/distance/piste, note recalculée |
| 📡 Session | Création/gestion du code de session, synchronisation Firebase |
| ⚙ Gestion | Règles Firebase sécurisées, configuration, déconnexion |

### 🔴 Suivi en direct

- L'enseignant peut cliquer sur un élève actif → **fiche live** affichant chrono, tirs et LEDs en temps réel (rafraîchissement toutes les 3 s)
- Boutons de **pénalités en direct** : avertissement, +10 s, élimination, disqualification
- Notification instantanée sur le téléphone de l'élève

### 📊 Pages supplémentaires

- **Résultats** : tableau récapitulatif de tous les passages de la séance
- **Barèmes** : grilles de notation complètes (difficulté, course garçons/filles, tir, projet)

---

## 🛠 Technologies utilisées

| Technologie | Rôle |
|---|---|
| **HTML5 / CSS3** | Structure et design de l'interface (thème sombre, responsive mobile) |
| **JavaScript (ES6+)** | Logique métier, chronomètres, calcul des notes |
| **Firebase Realtime Database v9** | Synchronisation temps réel (présence, résultats, pénalités, live) |
| **Web Crypto API** | Chiffrement AES-256-GCM des passages, SHA-256 pour l'authentification |
| **Barlow / Barlow Condensed** | Polices Google Fonts |

> **Architecture** : Application 100 % client-side, zéro serveur backend. Un seul fichier HTML auto-suffisant.

---

## 🚀 Déploiement — GitHub Pages

### Prérequis

- Un compte GitHub
- Un projet Firebase (Realtime Database activé, région `europe-west1`)

### Étapes

```bash
# 1. Forker ou cloner le dépôt
git clone https://github.com/votre-compte/votre-repo.git

# 2. Renommer le fichier en index.html si nécessaire
mv laser-run-eps-v8-secure.html index.html

# 3. Pousser sur GitHub
git add index.html
git commit -m "Déploiement Laser Run EPS"
git push origin main
```

**4. Activer GitHub Pages :**  
`Settings` → `Pages` → `Source : Deploy from a branch` → `main / (root)` → **Save**

**5. URL du site :**  
`https://votre-compte.github.io/votre-repo/`

---

## 🔒 Configuration Firebase sécurisée (obligatoire)

Dans la console Firebase ([console.firebase.google.com](https://console.firebase.google.com)) :  
**Realtime Database → Règles → Remplacer par** :

```json
{
  "rules": {
    "sessions": {
      "$session_id": {
        "passages": {
          "$passage_id": {
            ".read": false,
            ".write": "!data.exists()"
          }
        },
        "live":     { ".read": true, ".write": true },
        "presence": { ".read": true, ".write": true },
        "penalties":{ ".read": true, ".write": true }
      }
    }
  }
}
```

> ⚠️ La règle `"!data.exists()"` empêche toute modification d'un passage après soumission.  
> Sans cette étape, les notes pourraient être altérées.

---

## 📱 Instructions d'utilisation

### Pour l'enseignant

1. Ouvrir l'application → onglet **👨‍🏫 Enseignant**
2. Saisir le mot de passe enseignant
3. Onglet **📡 Session** → générer ou saisir un code → **Démarrer**
4. Communiquer le code aux élèves
5. Suivre les passages depuis **🟢 Présence** (suivi live) ou **📋 Résultats** (notes finales)

### Pour l'élève

1. Ouvrir l'URL du site sur son smartphone
2. Onglet **🎯 Passage** → saisir le code de session donné par l'enseignant
3. Remplir les informations personnelles (nom, parcours, distance de tir, piste, temps projet)
4. Lancer le chronomètre → effectuer les 3 passages de tir
5. Une fois les 3 passages validés → courir jusqu'à la ligne d'arrivée → appuyer sur **🏁 Arrivée**
6. Vérifier la note → **Enregistrer & Synchroniser**

---

## 🛡 Note de sécurité

Le code JavaScript de cette application est **intentionnellement protégé** par plusieurs couches de sécurité :

| Couche | Description |
|---|---|
| **Chiffrement XOR + Base64** | Le code source JS est fragmenté en 1 400+ segments encodés |
| **Clé reconstituée dynamiquement** | La clé de déchiffrement est assemblée depuis 3 fragments séparés |
| **Vérification d'intégrité** | Un checksum est calculé à chaque chargement — toute modification déclenche `ERR_INTEGRITY_FAILED` |
| **Verrou de domaine** | L'application refuse de s'exécuter hors de son domaine autorisé (`ERR_DOMAIN_MISMATCH`) |
| **Anti-debug** | Détection des outils de développement ouverts |
| **AES-256-GCM** | Les données élèves sont chiffrées avant envoi à Firebase |
| **SHA-256** | Le mot de passe enseignant est haché de façon irréversible |
| **Données anonymisées** | Les noms complets ne sont jamais envoyés en clair dans Firebase |

> Ces protections sont mises en place pour **préserver la confidentialité des données scolaires** et **prévenir toute manipulation de notes** par les élèves.

---

## ⚖️ Propriété intellectuelle et avertissement

```
AVERTISSEMENT — PROPRIÉTÉ INTELLECTUELLE

Ce fichier et son contenu sont protégés.
Toute tentative de :
  - déobfuscation ou déchiffrement du code
  - réutilisation à des fins commerciales sans autorisation
  - modification et redistribution sans accord explicite de l'auteur

...est strictement interdite et susceptible d'engager la responsabilité
civile et/ou pénale de son auteur.

Ce projet est destiné exclusivement à un usage pédagogique en établissement scolaire.
```

---

## 📊 Conformité RGPD

| Point | Statut |
|---|---|
| Données minimales collectées | ✅ Prénom, nom, résultats sportifs uniquement |
| Hébergement Europe | ✅ Firebase `europe-west1` |
| Chiffrement des données | ✅ AES-256-GCM avant tout envoi |
| Noms anonymisés dans la base | ✅ Initiales uniquement dans `/live` et `/presence` |
| Durée de conservation | ⚠️ À effacer manuellement en fin d'année scolaire |
| Information des élèves | ⚠️ À réaliser oralement en début de séance |

---

## 📄 Licence

```
© 2026 — Projet Laser Run EPS
Tous droits réservés.
Usage pédagogique exclusif — lycée EPSMrMORAUX
```

---

*Généré et maintenu dans le cadre de l'enseignement de l'EPS.*  
*Déployé via GitHub Pages — [epsmrmoraux-web.github.io/EPS.Laser.run](https://epsmrmoraux-web.github.io/EPS.Laser.run/)*
