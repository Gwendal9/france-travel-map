# 🗺️ Ma Carte de France Interactive

Application web interactive pour suivre et planifier vos voyages à travers la France. Notez vos visites, planifiez vos futurs trips, et suivez votre progression département par département.

## 🚀 Tester l'application

### Option 1 : Accès direct via GitHub Pages (Recommandé)

**👉 [Ouvrir l'application](https://gwendal9.github.io/france-travel-map/)**

### Option 2 : En local

```bash
# Cloner le repo
git clone https://github.com/Gwendal9/france-travel-map.git
cd france-travel-map

# Ouvrir index.html dans votre navigateur
# Sur Mac:
open index.html

# Sur Linux:
xdg-open index.html

# Sur Windows:
start index.html
```

**Note** : Aucune installation ou compilation nécessaire ! L'application fonctionne directement dans le navigateur.

## 📋 Table des matières

- [Aperçu](#aperçu)
- [Technologies](#technologies)
- [Structure du projet](#structure-du-projet)
- [Features](#features)
- [Architecture des données](#architecture-des-données)
- [Guide de développement](#guide-de-développement)
- [API et Sources externes](#api-et-sources-externes)
- [Personnalisation](#personnalisation)
- [Roadmap](#roadmap)

---

## 🎯 Aperçu

### Fonctionnalités principales

- **Carte interactive** : 96 départements métropolitains + Corse avec formes géographiques réelles
- **Système de notation** : Notez chaque département de 1 à 5 étoiles via une barre interactive
- **Tracking des visites** : 4 niveaux (non visité, une nuit, une semaine, régulièrement)
- **Villes visitées** : Marquez les villes avec des points sur la carte
- **Wishlist** : Créez une liste d'idées par département
- **Planning** : Planifiez vos futurs voyages avec dates
- **Statistiques avancées** : Progression par région, top départements, distribution des notes

### Screenshots conceptuels

```
┌─────────────────────────────────────────────┐
│  🗺️ Carte | 📊 Stats | 📅 Planning | ⭐ Wishlist │
├─────────────────────────────────────────────┤
│                                              │
│         [Carte de France interactive]        │
│                                              │
│  Stats: 45/96 depts | 47% | Note moy: 3.8   │
└─────────────────────────────────────────────┘
```

---

## 🛠️ Technologies

### Stack technique

- **React 18** (via CDN - pas de build nécessaire)
- **Tailwind CSS** (via CDN)
- **Babel Standalone** (pour JSX)
- **localStorage** (persistence des données)
- **GeoJSON** (formes géographiques)

### Format du projet

**Application single-page HTML standalone**
- Fichier unique : `index.html`
- Aucun build process requis
- Ouvrir directement dans un navigateur

### Pourquoi ce choix ?

✅ Simplicité : un seul fichier
✅ Portabilité : fonctionne partout
✅ Pas de dépendances npm
✅ Facile à partager et modifier

---

## 📁 Structure du projet

```
index.html
├── <head>
│   ├── React 18 (CDN)
│   ├── ReactDOM 18 (CDN)
│   ├── Babel Standalone (CDN)
│   ├── Tailwind CSS (CDN)
│   └── Styles CSS personnalisés
│
└── <body>
    └── <script type="text/babel">
        ├── Constantes
        │   ├── GEOJSON_URL
        │   ├── departmentInfo (villes par département)
        │   ├── VISIT_LEVELS
        │   └── REGIONS
        │
        ├── Composants React
        │   ├── FranceMap (composant principal)
        │   ├── TabButton
        │   ├── MapView
        │   ├── StatsView
        │   ├── PlanningView
        │   ├── WishlistView
        │   ├── TripCard
        │   ├── StatItem
        │   ├── StatCard
        │   └── DepartmentModal
        │
        └── Logique
            ├── État React (appState, plannedTrips)
            ├── Gestion localStorage
            ├── Conversion GeoJSON → SVG
            └── Calculs statistiques
```

---

## ✨ Features

### 1. Carte Interactive

#### Départements
- **96 départements** métropolitains + Corse (2A, 2B)
- **Formes réelles** via GeoJSON
- **4 niveaux de visite** avec code couleur :
  - Gris foncé : Non visité
  - Bleu clair : Une nuit
  - Bleu moyen : Une semaine
  - Bleu foncé : Régulièrement

#### Effets visuels
- Texture de carte avec grille subtile
- Fond océan en arrière-plan
- Ombres portées sur départements
- Effet de relief au survol
- Transitions fluides

#### Villes visitées
- **Points rouges** sur la carte
- **Placement intelligent** :
  - 1 ville → centre du département
  - 2-4 villes → disposition en cercle
  - 5+ villes → spirale dorée
- **Animation de pulsation**
- **Tooltip** au survol avec nom de la ville

### 2. Système de notation ⭐

#### Interface
- **Barre horizontale interactive**
- Dégradé de couleur (gris → jaune)
- Clic n'importe où pour noter
- Affichage de la note (X/5)
- Bouton d'effacement rapide

#### Stockage
```javascript
rating: 0-5 // 0 = pas noté
```

### 3. Wishlist 🎯

Par département :
- Liste d'idées/activités à faire
- Ajout/suppression facile
- Vue dédiée avec tous les départements en wishlist
- Indicateur "Visité" si déjà fait

**Cas d'usage** :
- "Visiter le château de..."
- "Faire du vélo le long de..."
- "Goûter la spécialité locale"

### 4. Planning 📅

#### Fonctionnalités
- Planification de voyages futurs
- Dates de début/fin
- Notes (budget, idées, etc.)
- Séparation voyages à venir / passés
- Compte à rebours pour voyages proches (<7 jours)

#### Structure
```javascript
{
  id: timestamp,
  name: "Nom du voyage",
  startDate: "2026-03-15",
  endDate: "2026-03-17", // optionnel
  notes: "Budget 500€, réserver hôtel"
}
```

### 5. Statistiques 📊

#### Globales
- Départements visités (X/96)
- Pourcentage de la France
- Visites régulières
- Villes visitées
- Note moyenne
- Départements en wishlist
- Régions complètes

#### Par région
- **13 régions administratives**
- Barre de progression
- Pourcentage de complétion
- Mise en évidence des régions 100%

#### Top 10
- Départements les mieux notés
- Classement avec podium
- Affichage des étoiles

#### Distribution des notes
- Graphique horizontal
- Nombre de départements par note
- Visualisation de la tendance

---

## 💾 Architecture des données

### localStorage Keys

```javascript
// État principal (Version 2)
localStorage.getItem('franceMapStateV2')

// Voyages planifiés
localStorage.getItem('franceMapPlannedTrips')
```

### Structure appState

```javascript
{
  "01": {
    visitLevel: "regular", // "unvisited" | "one-night" | "one-week" | "regular"
    visitedCities: ["Bourg-en-Bresse", "Oyonnax"],
    customCities: ["Petit village perdu"],
    notes: "Super week-end, très beau château",
    rating: 4, // 0-5
    wishlist: [
      "Visiter le lac de Nantua",
      "Faire du vélo dans les montagnes"
    ]
  },
  "02": { ... },
  // ... 96 départements
}
```

### Structure plannedTrips

```javascript
[
  {
    id: 1234567890, // timestamp
    name: "Week-end Bretagne",
    startDate: "2026-03-15",
    endDate: "2026-03-17",
    notes: "Budget 500€, réserver hôtel à Saint-Malo"
  },
  { ... }
]
```

### Départements Info (constante)

```javascript
const departmentInfo = {
  '01': { 
    name: 'Ain', 
    cities: ['Bourg-en-Bresse', 'Oyonnax', 'Belley', 'Gex', 'Nantua'] 
  },
  // ... 96 départements avec 5 villes principales chacun
}
```

### Régions (constante)

```javascript
const REGIONS = {
  'Auvergne-Rhône-Alpes': ['01', '03', '07', '15', '26', '38', '42', '43', '63', '69', '73', '74'],
  'Bourgogne-Franche-Comté': ['21', '25', '39', '58', '70', '71', '89', '90'],
  'Bretagne': ['22', '29', '35', '56'],
  'Centre-Val de Loire': ['18', '28', '36', '37', '41', '45'],
  'Corse': ['2A', '2B'],
  'Grand Est': ['08', '10', '51', '52', '54', '55', '57', '67', '68', '88'],
  'Hauts-de-France': ['02', '59', '60', '62', '80'],
  'Île-de-France': ['75', '77', '78', '91', '92', '93', '94', '95'],
  'Normandie': ['14', '27', '50', '61', '76'],
  'Nouvelle-Aquitaine': ['16', '17', '19', '23', '24', '33', '40', '47', '64', '79', '86', '87'],
  'Occitanie': ['09', '11', '12', '30', '31', '32', '34', '46', '48', '65', '66', '81', '82'],
  'Pays de la Loire': ['44', '49', '53', '72', '85'],
  'Provence-Alpes-Côte d\'Azur': ['04', '05', '06', '13', '83', '84']
};
```

---

## 🔧 Guide de développement

### Prérequis

- Navigateur moderne (Chrome, Firefox, Safari, Edge)
- Éditeur de texte (VS Code recommandé)
- Connexion internet (pour charger les CDN et GeoJSON)

### Installation

```bash
# Aucune installation nécessaire !
# Télécharger le fichier et l'ouvrir dans un navigateur
```

### Développement local

1. Ouvrir `index.html` dans un navigateur
2. Modifier le code
3. Rafraîchir la page (F5)
4. Les données localStorage persistent entre les rechargements

### Structure du code React

#### Composant principal

```javascript
function FranceMap() {
  // États
  const [geoData, setGeoData] = useState(null);
  const [appState, setAppState] = useState(() => { /* init from localStorage */ });
  const [plannedTrips, setPlannedTrips] = useState(() => { /* init from localStorage */ });
  const [modalOpen, setModalOpen] = useState(false);
  const [currentDepartment, setCurrentDepartment] = useState(null);
  const [activeTab, setActiveTab] = useState('map');

  // Effects
  useEffect(() => { /* Charger GeoJSON */ }, []);
  useEffect(() => { /* Sauvegarder appState */ }, [appState]);
  useEffect(() => { /* Sauvegarder plannedTrips */ }, [plannedTrips]);

  // Fonctions
  const openModal = (code) => { /* ... */ };
  const closeModal = () => { /* ... */ };
  const updateDepartment = (code, updates) => { /* ... */ };

  // Statistiques calculées
  const stats = { /* ... */ };

  // Render
  return ( /* ... */ );
}
```

#### Conversion GeoJSON → SVG

```javascript
const convertToSVGPath = (coordinates, bounds) => {
  // 1. Projeter les coordonnées géographiques (lon, lat) en pixels (x, y)
  const projectPoint = ([lon, lat]) => {
    const x = ((lon - bounds.minLon) / (bounds.maxLon - bounds.minLon)) * 1000;
    const y = ((bounds.maxLat - lat) / (bounds.maxLat - bounds.minLat)) * 1100;
    return [x, y];
  };

  // 2. Créer un path SVG (M = move to, L = line to, Z = close)
  const processRing = (ring) => {
    const projected = ring.map(projectPoint);
    return 'M ' + projected.map(p => p.join(',')).join(' L ') + ' Z';
  };

  // 3. Gérer Polygon et MultiPolygon
  // ...
};
```

#### Placement intelligent des villes

```javascript
// Algorithme adaptatif selon le nombre de villes
if (state.visitedCities.length === 1) {
  // Au centre
  cityX = x;
  cityY = y;
} else if (state.visitedCities.length <= 4) {
  // Cercle régulier
  const angle = (idx / state.visitedCities.length) * 2 * Math.PI;
  cityX = x + Math.cos(angle) * radius;
  cityY = y + Math.sin(angle) * radius;
} else {
  // Spirale dorée (optimal pour 5+)
  const spiralRadius = radius * (0.3 + (idx / state.visitedCities.length) * 0.7);
  const angle = idx * (Math.PI * 2 / 3); // Angle d'or
  cityX = x + Math.cos(angle) * spiralRadius;
  cityY = y + Math.sin(angle) * spiralRadius;
}
```

### Debugging

#### Console browser

```javascript
// Voir l'état actuel
console.log(JSON.parse(localStorage.getItem('franceMapStateV2')));

// Réinitialiser les données
localStorage.removeItem('franceMapStateV2');
localStorage.removeItem('franceMapPlannedTrips');

// Vérifier les données GeoJSON
fetch('https://raw.githubusercontent.com/gregoiredavid/france-geojson/master/departements-version-simplifiee.geojson')
  .then(r => r.json())
  .then(d => console.log(d));
```

#### Erreurs communes

**La carte ne s'affiche pas**
- Vérifier la connexion internet (GeoJSON distant)
- Console : erreur CORS ? → Utiliser un serveur local
- GeoJSON mal chargé ? → Vérifier l'URL

**Les données ne sont pas sauvegardées**
- localStorage désactivé ? → Vérifier les paramètres du navigateur
- Mode privé ? → Les données sont perdues à la fermeture

**Performance lente**
- Trop de villes affichées ? → Limiter à ~10 par département
- SVG trop complexe ? → Utiliser GeoJSON simplifié

---

## 🌐 API et Sources externes

### GeoJSON - Formes des départements

**URL** : `https://raw.githubusercontent.com/gregoiredavid/france-geojson/master/departements-version-simplifiee.geojson`

**Source** : [gregoiredavid/france-geojson](https://github.com/gregoiredavid/france-geojson)

**Structure** :
```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "code": "01",
        "nom": "Ain"
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[lon, lat], [lon, lat], ...]]
      }
    },
    ...
  ]
}
```

**Alternatives** :
- Version détaillée : `.../departements.geojson`
- Version très simplifiée : `.../departements-version-simplifiee.geojson` (actuelle)

### CDN utilisés

```html
<!-- React 18 -->
<script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>

<!-- Babel Standalone (JSX) -->
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

<!-- Tailwind CSS -->
<script src="https://cdn.tailwindcss.com"></script>
```

---

## 🎨 Personnalisation

### Couleurs des régions

```javascript
const REGION_COLORS = {
  'Auvergne-Rhône-Alpes': { r: 52, g: 152, b: 219 },      // Bleu
  'Bourgogne-Franche-Comté': { r: 155, g: 89, b: 182 },   // Violet
  'Bretagne': { r: 46, g: 204, b: 113 },                  // Vert
  'Centre-Val de Loire': { r: 241, g: 196, b: 15 },       // Jaune
  'Corse': { r: 230, g: 126, b: 34 },                     // Orange
  'Grand Est': { r: 231, g: 76, b: 60 },                  // Rouge
  'Hauts-de-France': { r: 52, g: 73, b: 94 },             // Bleu foncé
  'Île-de-France': { r: 149, g: 165, b: 166 },            // Gris
  'Normandie': { r: 26, g: 188, b: 156 },                 // Turquoise
  'Nouvelle-Aquitaine': { r: 142, g: 68, b: 173 },        // Pourpre
  'Occitanie': { r: 243, g: 156, b: 18 },                 // Orange doré
  'Pays de la Loire': { r: 22, g: 160, b: 133 },          // Vert sarcelle
  'Provence-Alpes-Côte d\'Azur': { r: 211, g: 84, b: 0 }  // Orange brûlé
};
```

**Modifier** : Changer les valeurs RGB pour personnaliser les couleurs de chaque région.

**Note** : L'intensité de la couleur est automatiquement calculée en fonction du pourcentage de villes visitées dans chaque département.

### Villes par défaut

```javascript
const departmentInfo = {
  '01': { 
    name: 'Ain', 
    cities: ['Bourg-en-Bresse', 'Oyonnax', 'Belley', 'Gex', 'Nantua'] 
  },
  // Modifier la liste des villes ici
}
```

### Texture de la carte

```css
.map-container::before {
  background-image: 
    repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px),
    repeating-linear-gradient(90deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
}
```

**Modifier** : Ajuster `2px` et `4px` pour changer la densité de la grille

### Animation des villes

```css
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.8; transform: scale(1.1); }
}
```

**Modifier** : Ajuster les valeurs de `scale` et `opacity`

---

## 🚀 Roadmap

### Features à implémenter

#### Priorité HAUTE

- [ ] **Photos par département**
  - Upload d'images
  - Galerie avec lightbox
  - Légendes
  - Stockage base64 ou Firebase

- [ ] **Itinéraires**
  - Tracer des routes sur la carte
  - Départements traversés
  - Distance estimée
  - Mode vélo/voiture

- [ ] **Export/Import**
  - Export JSON des données
  - Import depuis fichier
  - Backup automatique
  - Partage avec d'autres utilisateurs

- [ ] **Highlights par département**
  - Moments mémorables
  - Dates importantes
  - Anecdotes
  - Meilleurs souvenirs

#### Priorité MOYENNE

- [ ] **Mode sombre**
  - Toggle dark/light
  - Sauvegarde de préférence
  - Couleurs adaptées

- [ ] **Graphiques temporels**
  - Évolution des visites dans le temps
  - Timeline
  - Heatmap par mois/année

- [ ] **Filtres et recherche**
  - Rechercher un département
  - Filtrer par note
  - Filtrer par région
  - Filtrer par wishlist

- [ ] **Comparaisons**
  - Comparer avec d'autres utilisateurs
  - Statistiques nationales
  - Défis/achievements

#### Priorité BASSE

- [ ] **Intégrations**
  - Strava (trajets vélo)
  - Google Photos (photos auto)
  - Instagram (publications)

- [ ] **Partage social**
  - Génération d'image de la carte
  - Badges de réussite
  - Stories Instagram

- [ ] **Multi-utilisateurs**
  - Compte utilisateur
  - Cloud sync
  - Collaborative maps

### Améliorations techniques

- [ ] **Migration vers projet React standard**
  - Create React App ou Vite
  - npm packages
  - Build optimisé

- [ ] **Tests**
  - Unit tests (Jest)
  - E2E tests (Cypress)
  - Tests de performance

- [ ] **Accessibilité**
  - Support clavier complet
  - Screen readers
  - WCAG 2.1 AA

- [ ] **PWA**
  - Service Worker
  - Mode offline
  - Installation sur mobile

---

## 📝 Notes de développement

### Limitations actuelles

1. **Taille localStorage** : ~5-10 MB selon navigateur
   - Problème si beaucoup de photos
   - Solution : Firebase/Supabase pour images

2. **GeoJSON distant** : Nécessite connexion internet
   - Solution : Embarquer le GeoJSON dans le HTML

3. **Pas de sync multi-device**
   - Solution : Backend avec authentification

4. **Format standalone** : Moins maintenable à grande échelle
   - Solution : Migrer vers projet React standard

### Bonnes pratiques

#### Gestion d'état
```javascript
// ✅ Bon : Mise à jour immutable
setAppState(prev => ({
  ...prev,
  [code]: { ...prev[code], rating: 5 }
}));

// ❌ Mauvais : Mutation directe
appState[code].rating = 5;
setAppState(appState);
```

#### Performance
```javascript
// ✅ Bon : Mémorisation des calculs
const stats = useMemo(() => calculateStats(appState), [appState]);

// ❌ Mauvais : Calcul à chaque render
const stats = calculateStats(appState);
```

#### localStorage
```javascript
// ✅ Bon : Try-catch pour erreurs
try {
  localStorage.setItem('key', JSON.stringify(data));
} catch (e) {
  console.error('Storage error:', e);
  // Fallback ou notification utilisateur
}

// ❌ Mauvais : Pas de gestion d'erreur
localStorage.setItem('key', JSON.stringify(data));
```

---

## 🤝 Contribution

### Pour Claude Code

**Contexte à fournir** :
```
Projet : Carte interactive de France (React standalone)
Fichier : index.html
Tech : React 18 CDN, Tailwind CSS, GeoJSON
```

**Guidelines** :
- Garder le format single-file HTML
- Utiliser React hooks (pas de classes)
- Préférer Tailwind aux CSS custom
- Commenter les fonctions complexes
- Tester dans plusieurs navigateurs

### Demandes courantes

**"Ajouter une feature X"**
1. Identifier où dans le code (quel composant)
2. Vérifier si localStorage nécessaire
3. Tester avec données réelles
4. Documenter dans ce README

**"Corriger un bug"**
1. Reproduire le bug
2. Console logs pour debug
3. Identifier la cause
4. Fix + test
5. Commit avec description

**"Améliorer les performances"**
1. Profiler avec DevTools
2. Identifier les re-renders inutiles
3. Ajouter useMemo/useCallback
4. Tester l'amélioration

---

## 📞 Support

### Ressources

- **React Docs** : https://react.dev
- **Tailwind CSS** : https://tailwindcss.com
- **GeoJSON Spec** : https://geojson.org
- **SVG Path** : https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths

### Troubleshooting

**Q: La carte est vide**
A: Vérifier la console pour erreurs GeoJSON. Tester l'URL manuellement.

**Q: Les données ne se sauvent pas**
A: Vérifier que localStorage n'est pas désactivé. Mode privé ?

**Q: Performance lente**
A: Limiter le nombre de villes affichées. Simplifier le GeoJSON.

**Q: Les villes sont mal placées**
A: Vérifier le calcul du centroïde. Ajuster le rayon adaptatif.

---

## 📄 Licence

Projet personnel - Utilisation libre

**Crédits** :
- Données GeoJSON : [gregoiredavid/france-geojson](https://github.com/gregoiredavid/france-geojson)
- React : Meta/Facebook
- Tailwind CSS : Tailwind Labs

---

## 🎉 Changelog

### v2.1 (Actuelle)
- ✨ **Coloration par région** : Chaque département est coloré selon sa région (13 couleurs distinctes)
- ✨ **Intensité dynamique** : La couleur devient plus vive en fonction du % de villes visitées (0% = très pâle, 100% = couleur pleine)
- ✨ **Coordonnées GPS réelles** : Plus de 100 villes principales positionnées à leurs vraies coordonnées géographiques
- 🎨 Légende améliorée avec explication du système de coloration par région
- 🎨 Tooltips enrichis affichant le pourcentage de villes visitées
- 📍 Marqueurs de villes plus précis et visibles

### v2.0
- ✨ Système de notation avec barre interactive
- ✨ Wishlist par département
- ✨ Planning de voyages
- ✨ Statistiques avancées (progression régions, top 10, distribution)
- 🎨 Texture de carte améliorée
- 🎨 Placement intelligent des villes (spirale adaptative)
- 🐛 Correction bugs localStorage

### v1.0
- 🎉 Version initiale
- 🗺️ Carte interactive avec vraies formes
- 📍 Marqueurs de villes
- 📝 Notes par département
- 💾 Sauvegarde localStorage

---

**Dernière mise à jour** : Janvier 2026
**Version** : 2.0
**Auteur** : Gwendal
