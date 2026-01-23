# 🗺️ Carte Interactive de France

Application web interactive pour suivre votre découverte de la France. Marquez vos visites ville par ville, département par département, et visualisez votre progression à travers le pays.

## 🚀 Utilisation

**👉 [Ouvrir l'application](https://gwendal9.github.io/france-travel-map/)**

Ou en local :
```bash
git clone https://github.com/Gwendal9/france-travel-map.git
cd france-travel-map
open index.html  # ou double-clic sur le fichier
```

**Note** : Aucune installation nécessaire ! L'application fonctionne directement dans le navigateur.

---

## ✨ Fonctionnalités

### 🗺️ Carte interactive
- **96 départements** avec leurs vraies formes géographiques
- **Coloration par région** : 13 régions françaises avec des couleurs distinctes
- **Transparence dynamique** : Plus vous avez visité un département, plus il devient opaque et coloré
- **Mini-carte Île-de-France** : Zoom sur les 8 départements de la région parisienne

### 📍 Suivi des villes
- **4 niveaux de visite** pour chaque ville :
  - ⚪ **Jamais allé** : Ville non visitée (gris)
  - 🟡 **Déjà passé** : Simple passage dans la ville (orange)
  - 🟢 **Déjà mangé** : Repas dans la ville (vert)
  - 🟣 **Déjà dormi** : Nuit passée dans la ville (violet)

- **~500 villes** pré-enregistrées avec leurs coordonnées GPS réelles
- **10 villes principales** par département (par population)
- **Affichage sur la carte** : Les villes visitées apparaissent comme des points colorés
- **Sélection ultra-minimaliste** : Clic sur une ville → choix parmi 4 cercles de couleur

### 🎨 Visualisation intelligente
- **Intensité par niveau maximum** : La couleur du département reflète votre niveau de visite le plus élevé
  - Passé → 50% d'opacité
  - Mangé → 75% d'opacité
  - Dormi → 100% d'opacité (couleur pleine)
- **Marqueurs sur carte principale** : Toutes les villes visitées visibles d'un coup d'œil
- **Vue détaillée** : Cliquez sur un département pour voir et marquer ses villes

### 💾 Sauvegarde automatique
- Données enregistrées localement dans votre navigateur (localStorage)
- Aucun compte requis, confidentialité totale
- Les données persistent entre les sessions

---

## 🛠️ Technologies

Application **single-page HTML standalone** :
- **React 18** (via CDN)
- **Tailwind CSS** (via CDN)
- **GeoJSON** (formes géographiques réelles)
- **localStorage** (sauvegarde des données)

**Avantages** :
- ✅ Un seul fichier `index.html`
- ✅ Pas de build, pas de npm
- ✅ Fonctionne partout, modifiable facilement
- ✅ Totalement gratuit et open-source

---

## 📊 Structure des données

### Stockage localStorage

```javascript
{
  "01": {  // Code département (Ain)
    cityVisits: {
      "Bourg-en-Bresse": "slept",    // 🟣 Dormi
      "Oyonnax": "ate",               // 🟢 Mangé
      "Belley": "passed",             // 🟡 Passé
      "Nantua": "never"               // ⚪ Jamais (par défaut)
    }
  },
  "02": { ... },
  // ... 96 départements
}
```

### Départements couverts

- **France métropolitaine** : 96 départements
- **Régions** : 13 régions administratives
- **Villes** : ~500 villes avec GPS précis

---

## 🎨 Personnalisation

### Couleurs des régions

Chaque région a sa propre couleur :
- 🔵 **Auvergne-Rhône-Alpes** : Bleu
- 🟣 **Bourgogne-Franche-Comté** : Violet
- 🟢 **Bretagne** : Vert
- 🟡 **Centre-Val de Loire** : Jaune
- 🟠 **Corse** : Orange
- 🔴 **Grand Est** : Rouge
- 🔵 **Hauts-de-France** : Bleu foncé
- ⚫ **Île-de-France** : Gris
- 🔷 **Normandie** : Turquoise
- 🟣 **Nouvelle-Aquitaine** : Pourpre
- 🟠 **Occitanie** : Orange doré
- 🟢 **Pays de la Loire** : Vert sarcelle
- 🟠 **PACA** : Orange brûlé

Les couleurs s'intensifient automatiquement selon votre niveau de visite.

---

## 📝 Développement

### Modifier le code

1. Ouvrir `index.html` dans un éditeur de texte
2. Modifier le code React/CSS
3. Sauvegarder
4. Rafraîchir la page dans le navigateur (F5)

### Structure du fichier

```
index.html
├── <head>
│   ├── CDN React, Tailwind, Babel
│   └── Styles CSS personnalisés
│
└── <script type="text/babel">
    ├── CITY_COORDINATES (500+ villes GPS)
    ├── departmentInfo (10 villes/département)
    ├── VISIT_LEVELS (4 niveaux de visite)
    ├── REGIONS (13 régions)
    ├── REGION_COLORS (couleurs par région)
    │
    ├── Composant FranceMap
    ├── Composant MapView
    └── Composant DepartmentOverlay
```

### Debug

```javascript
// Console navigateur
// Voir toutes les données
console.log(JSON.parse(localStorage.getItem('franceMapCityVisits')));

// Réinitialiser
localStorage.removeItem('franceMapCityVisits');
location.reload();
```

---

## 🚀 Roadmap

### À venir
- [ ] Export/Import des données (JSON)
- [ ] Statistiques avancées (% par région, graphiques)
- [ ] Ajout de villes personnalisées
- [ ] Mode sombre
- [ ] Partage de carte (image/lien)
- [ ] PWA pour utilisation offline

### Idées futures
- [ ] Intégration photos par ville
- [ ] Carnets de voyage
- [ ] Chronologie des visites
- [ ] Comparaison avec amis

---

## 📄 Crédits & Licence

**Projet** : Libre d'utilisation

**Données géographiques** :
- GeoJSON France : [gregoiredavid/france-geojson](https://github.com/gregoiredavid/france-geojson)

**Technologies** :
- React (Meta)
- Tailwind CSS (Tailwind Labs)
- Babel Standalone

---

## 🎉 Changelog

### v3.0 (Janvier 2026) - Version actuelle
- ✨ **Système de visite 4 niveaux** : Jamais/Passé/Mangé/Dormi
- ✨ **500+ villes GPS** : Coordonnées précises de toutes les villes principales
- ✨ **10 villes par département** : Couverture complète de la France
- ✨ **Mini-carte Île-de-France** : Zoom sur Paris et sa région en haut à gauche
- ✨ **Sélection minimaliste** : Interface ultra-simple avec 4 cercles colorés
- 🎨 **Transparence par niveau max** : Couleur basée sur votre meilleur niveau de visite
- 🎨 **Marqueurs sur carte principale** : Toutes vos visites visibles en un coup d'œil
- 🎨 **Fenêtre agrandie** : Vue département à 98% de l'écran (1800px)
- 🐛 **Correction chevauchement** : Pas de superposition au survol
- 🗑️ **Suppression** : Wishlist et planning (simplification)

### v2.1
- ✨ Coloration par région (13 couleurs)
- ✨ Intensité dynamique selon % villes visitées
- ✨ 100+ villes GPS réelles
- 🎨 Légende améliorée

### v2.0
- ✨ Système de notation
- ✨ Wishlist et planning
- ✨ Statistiques avancées

### v1.0
- 🎉 Version initiale
- 🗺️ Carte interactive
- 📍 Marqueurs de villes

---

**Dernière mise à jour** : Janvier 2026
**Version** : 3.0
**Auteur** : Gwendal
