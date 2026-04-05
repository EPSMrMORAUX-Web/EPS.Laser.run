# 🎯 Laser Run EPS

Application web d'évaluation du **Laser Run** pour les cours d'EPS.  
Conçue pour fonctionner **hors connexion**, sur **mobile et ordinateur**, en un seul fichier HTML — aucune installation requise.

---

## 📋 Présentation

Le Laser Run est une activité combinant course à pied et tir laser. Cette application permet à chaque élève de **chronomètrer son passage**, de **saisir ses résultats de tir**, et d'obtenir une **note automatique**. L'enseignant regroupe ensuite tous les résultats sur sa tablette via un **code de session partagé** ou en **scannant les QR codes** des élèves.

---

## 🚀 Déploiement

### Option A — GitHub Pages (recommandé)

1. Créez un dépôt GitHub (ex : `laser-run-eps`)
2. Déposez le fichier `laser-run-eps-v5.html` à la racine, **renommé `index.html`**
3. Dans les paramètres du dépôt → **Pages** → Source : `main` / `root`
4. Votre application est accessible à l'adresse :
   ```
   https://VOTRE-COMPTE.github.io/laser-run-eps/
   ```
5. Dans l'application → Espace Enseignant → Gestion → renseignez cette URL pour générer le QR code d'accès

### Option B — Utilisation locale

Double-cliquez sur le fichier `laser-run-eps-v5.html` dans n'importe quel navigateur moderne. Aucune connexion internet nécessaire (sauf pour les polices Google Fonts au premier chargement).

---

## 📱 Accès pour les élèves

### En début de séance

1. Ouvrez l'application sur votre tablette
2. Allez dans **Espace Enseignant → Gestion**
3. Un **QR code de l'URL** de l'application s'affiche
4. Projetez-le ou montrez-le aux élèves — ils le scannent avec leur téléphone pour accéder directement à l'app

> **Astuce :** Ajoutez l'URL en favori sur votre ENT ou envoyez-la par message avant le cours.

---

## 🏃 Utilisation — Côté élève

### 1. Rejoindre la session
Quand l'élève arrive sur l'onglet **Passage**, une fenêtre lui propose de saisir le **code de session** donné par l'enseignant. Il peut aussi passer cette étape et utiliser l'application sans session.

### 2. Saisir les informations
- Prénom, Nom, Sexe
- **Parcours** (niveau 1 à 5 selon la combinaison course/distance de tir)
- **Temps de projet** annoncé avant le départ (facultatif, jusqu'à 2 pts bonus)

### 3. Effectuer le passage
- **Chronomètre général** : démarre au départ, tourne pendant toute l'épreuve
- **3 passages de tir** : chacun dispose de son propre chronomètre, d'un compteur de tirs et d'un sélecteur de LED allumées (0 à 5)
- Valider chaque passage une fois terminé

### 4. Résultats & QR code
Quand les 3 passages sont validés :
- Le récapitulatif et la **note automatique** s'affichent
- Un **QR code** est généré — l'élève le montre à l'enseignant pour un import instantané
- Si une session est active, le résultat est **automatiquement enregistré** sous le code de session

---

## 👨‍🏫 Utilisation — Côté enseignant

### Connexion
L'espace enseignant est protégé par un mot de passe. Lors de la première utilisation, vous en créez un. Il est stocké localement dans votre navigateur.

### Onglet Résultats
Tableau de bord complet de tous les passages importés :
- Nom, niveau, temps total, temps sur cible, temps de course
- Nombre de tirs, LED allumées, taux de réussite
- Notes détaillées (tir, course, projet) et note totale
- Note qualitative (1 à 4) saisie par l'enseignant
- Export PDF d'un clic

### Onglet Session 📡 *(méthode principale)*

**Créer une session :**
1. Générez un code (ou choisissez-en un simple : `1234`, `5678`…)
2. Cliquez **Démarrer la session**
3. Communiquez le code à vos élèves

**Récupérer les résultats :**
1. Une fois tous les passages effectués, allez dans **Récupérer les résultats**
2. Entrez le code de session
3. Cliquez **Importer** → tous les résultats apparaissent dans le tableau

> ⚠️ Cette méthode fonctionne sur le **même appareil** ou sur des appareils partageant le même navigateur/profil. Pour des téléphones différents, utilisez la méthode Scanner QR ci-dessous.

### Onglet Scanner QR 📷 *(méthode universelle)*

1. Cliquez **Démarrer la caméra** → autorisez l'accès à l'appareil photo
2. Pointez vers le QR code affiché sur le téléphone de l'élève
3. Le résultat s'importe automatiquement
4. Répétez pour chaque élève

> En cas d'échec de la caméra, utilisez le bouton **Coller un JSON manuellement** — l'élève copie son JSON et vous le transmet (message, mail…).

### Onglet Gestion
- **QR code d'accès** : générez et affichez le QR code de l'URL de l'application pour vos élèves
- **Changement de mot de passe**
- **Déconnexion**

---

## 🧮 Système de notation

La note totale est sur **15 points**, répartis ainsi :

| Critère | Barème | Détail |
|---|---|---|
| **Temps sur cible** | /8 | Temps cumulé des 3 passages de tir |
| **Temps de course** | /5 | Temps total − temps cible, normalisé selon le parcours |
| **Temps de projet** | /2 | Écart entre le temps annoncé et le temps réalisé |

### Pénalités tirs excessifs
| Nombre de tirs par passage | Pénalité |
|---|---|
| 10 à 12 tirs | −0,5 pt sur la note tir |
| 13 tirs ou plus | −1 pt sur la note tir |

### Parcours disponibles

| Niveau | Course | Distance de tir | Difficulté |
|---|---|---|---|
| 1 | A — 20m + 3×400m | 5m | ⭐ |
| 2 | A — 20m + 3×400m | 6m | ⭐⭐ |
| 3 | B — 20m + 3×500m | 6m | ⭐⭐⭐ |
| 4 | B — 20m + 3×500m | 7m | ⭐⭐⭐⭐ |
| 5 | C — 20m + 3×600m | 7m | ⭐⭐⭐⭐⭐ |

### Note qualitative (enseignant uniquement)
L'enseignant peut attribuer une note qualitative de 1 à 4 :

| Note | Label |
|---|---|
| 1 | Insuffisant |
| 2 | Fragile |
| 3 | Satisfaisant |
| 4 | Très bon |

---

## 🔄 Flux complet d'une séance

```
AVANT LE COURS
──────────────
Enseignant → Espace Enseignant → Session → Créer code "1234"
Enseignant → Gestion → Affiche QR code de l'app aux élèves

PENDANT LE COURS
─────────────────
Élève → Scanne QR → Ouvre l'app sur son téléphone
Élève → Onglet Passage → Saisit le code "1234"
Élève → Remplit ses infos → Lance le chronomètre
Élève → Effectue ses 3 passages de tir
Élève → Valide → Note calculée + QR code affiché

RÉCUPÉRATION
─────────────
Option 1 — Enseignant → Session → Importer → code "1234" → tous les résultats
Option 2 — Enseignant → Scanner QR → scanne le téléphone de chaque élève

FIN DE SÉANCE
──────────────
Enseignant → Résultats → Ajoute notes qualitatives → Export PDF
```

---

## 💾 Stockage des données

Toutes les données sont stockées dans le **localStorage** du navigateur, sans serveur externe.

| Clé | Contenu |
|---|---|
| `laserrun_v5` | Élèves et passages de l'appareil courant |
| `lr_session_XXXX` | Résultats associés au code de session XXXX |
| `lr_pw` | Mot de passe enseignant (texte brut) |
| `lr_active_session` | Code de session enseignant en cours |
| `lr_eleve_session` | Code de session élève mémorisé |
| `lr_app_url` | URL personnalisée pour le QR code d'accès |

> Les données persistent tant que le cache du navigateur n'est pas vidé.

---

## 🛠️ Compatibilité

| Navigateur | Support |
|---|---|
| Chrome / Chromium | ✅ Complet |
| Safari (iOS) | ✅ Complet |
| Firefox | ✅ Complet |
| Samsung Internet | ✅ Complet |
| Edge | ✅ Complet |

### Caméra (scanner QR)
La caméra nécessite :
- Un navigateur moderne supportant `getUserMedia`
- **HTTPS** obligatoire (GitHub Pages ✅ — fichier local ❌ sur certains navigateurs)
- L'autorisation explicite de l'utilisateur

---

## 📦 Dépendances

L'application est **quasi autonome**. Une seule librairie externe est chargée dynamiquement :

| Librairie | Usage | CDN |
|---|---|---|
| [jsQR](https://github.com/cozmo/jsQR) v1.4.0 | Lecture des QR codes via caméra | jsDelivr (fallback: unpkg) |

Le moteur de **génération QR** est embarqué directement dans le fichier HTML (code natif, aucune dépendance externe).

Les polices **Barlow / Barlow Condensed** sont chargées depuis Google Fonts (facultatif — l'app reste fonctionnelle sans connexion avec une police système).

---

## 📁 Structure du projet

```
laser-run-eps/
├── index.html          ← L'intégralité de l'application (renommer depuis laser-run-eps-v5.html)
└── README.md           ← Ce fichier
```

---

## ✏️ Personnalisation

Toutes les constantes pédagogiques sont définies en haut du bloc `<script>` :

```javascript
// Modifier les barèmes
const BAREME_CIBLE = [...];      // Barème temps sur cible → note /8
const BAREME_COURSE_M = [...];   // Barème course garçons → note /5
const BAREME_COURSE_F = [...];   // Barème course filles → note /5

// Modifier les parcours
const PARCOURS_INFO = {
  '1': { course: 'A (20m+3×400m)', tir: '5m', dist: 1200 },
  // ...
};
```

---

## 🔐 Sécurité

Le mot de passe enseignant est stocké en **texte brut** dans le localStorage. Il s'agit d'une protection légère contre un accès accidentel, non d'une sécurité cryptographique. Ne réutilisez pas un mot de passe sensible.

---

## 📄 Licence

Libre d'utilisation pour un usage éducatif. Aucune restriction pour l'enseignement EPS.
