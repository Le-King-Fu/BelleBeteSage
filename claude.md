# La Belle, la Bete et la Sage - Guide de développement

## Description
Jeu de type de style cyberpunk/neon où le joueur choisit un personnage (un chien) et doit attraper les pieces de monnaie dans l'une des 3 voies.
Il doit eviter les obstacles, soit en sautant par dessus les petits obstacles ou en changeant de voies.
Le joueur dispose de plusieurs vies et la difficulté augmente automatiquement tous les 1500 points.

## Stack technique
- **Build** : Vite 5.x
- **Tests** : Vitest avec couverture v8
- **Style** : Cyberpunk/neon avec effets de glow.
- **Audio** : Web Audio API (ondes carrées 8-bit)
- **Art**  : L'art est de style "pixel art"

## Architecture

```
src/
├── main.js          # Point d'entrée, initialisation, callbacks UI
├── game.js          # Boucle de jeu, états, vies, level up
├── config.js        # Constantes globales (couleurs, niveaux, touches, vies)
│
├── entities/
│   └── Note.js      # Entité note tombante
│
├── systems/
│   ├── Input.js     # Gestion clavier et tactile
│   ├── Renderer.js  # Rendu canvas avec effets neon
│   └── Audio.js     # Sons 8-bit
│
└── utils/
    └── helpers.js   # Fonctions utilitaires
```

## Conventions

### Code
- Commentaires en français
- Classes ES6 avec modules
- Noms de variables explicites en anglais
- JSDoc pour les fonctions publiques

### Style visuel - Cyberpunk/Neon Orange
- Résolution native : 320×240 - à réviser en fonction des autres caractéristiques du jeu
- Affichage upscalé ×2 : 640×480 - à réviser en fonction des autres caractéristiques du jeu
- Police : 'Courier New', monospace
- Thème sombre avec accents néon orange et vert
- Effets de glow (text-shadow, box-shadow)
- Animations pulse pour les éléments importants

### Tests
- Fichiers `*.test.js` dans `tests/`
- Couverture minimum : 70%
- Exécution : `npm test`

## Commandes

```bash
npm run dev          # Serveur de développement
npm run build        # Build production
npm test             # Lance les tests
npm run test:coverage # Tests avec couverture
```

## Palette de couleurs - Cyberpunk/Neon Orange

```javascript
COLORS = {
  BG: '#1a1a2e',           // Bleu-noir très foncé (fond principal)
  BG_SECONDARY: '#16213e', // Bleu nuit (fond secondaire)
  BG_DARK: '#0f3460',      // Bleu foncé (accents de fond)
  PRIMARY: '#ff6b35',      // Orange néon (éléments principaux, bordures)
  PRIMARY_DARK: '#e55a2b', // Orange foncé (ombres des boutons)
  SECONDARY: '#00ff88',    // Vert néon (score, succès, highlights)
  ACCENT: '#ff6b6b',       // Rouge clair (erreurs, vies)
  COIN: '#ffcc00',         // Or/jaune (bonus)
  TEXT: '#888888',         // Gris (texte secondaire)
  WHITE: '#ffffff'         // Blanc pur
}
```

## Gameplay

### Choix de personnages
- Flora, une chienne de type berger allemand
  - Force : 3/5
  - Vitesse : 4/5
  - Beauté : 5/5
- Nouki, un chien de type labrador dépeigné
  - Force : 5/5
  - Vitesse : 3/5
  - Beauté : 4/5
- Laska, un berger australien
  - Force : 3/5
  - Vitesse : 5/5
  - Beauté : 4/5
 
### Caractéristiques
  - La force donne le nombre de vie du chien
  - La vitesse donne sa vitesse de course (et donc, la vitesse a laquelle les points s'additionnent)
  - La beauté définie le multiplicateur de bonus
 
### Principes de base
- **-1 vie** à chaque obstacle touché
- Game over quand vies = 0
- Affichage : coeurs (♥♥♥♥♥) en fonction de la force du chien
- Les points augmentent avec la distance qui augmentent. la vitesse d'augmentation est en fonction de la vitesse.
- Chaque piece de monnaie ramassé donne 100 points.
- Les bonus donnent 500 x facteur de beauté.
- Les obstacles sont:
  - Petit (poubelles, cones, chat, rats, etc.) - Le joueur peut sauter par dessus.
  - Grand (Voiture, moto, vache, etc) - Le joueur ne peut pas sauter par dessus, il doit éviter.

### Difficulté croissante (Level Up)
- Tous les **2000 points**, le niveau augmente automatiquement
- Message **"LEVEL UP!"** affiché pendant 1 seconde
- 5 niveaux de difficulté : Débutant → Facile → Moyen → Difficile → Expert
- Vitesse et fréquence des obstacles augmentent à chaque niveau

### Niveaux
| Niveau    | Vitesse | Intervalle spawn |
|-----------|---------|------------------|
| Débutant  | 0.8     | 1600ms           |
| Facile    | 1.0     | 1300ms           |
| Moyen     | 1.3     | 1000ms           |
| Difficile | 1.6     | 800ms            |
| Expert    | 2.0     | 600ms            |

## Effets visuels

### Effets de glow (CSS)
```css
/* Titre et éléments principaux avec glow orange */
/* Score avec glow vert */
text-shadow: 0 0 5px #00ff88;

/* Canvas avec glow */
box-shadow: 0 0 20px rgba(255, 107, 53, 0.3);
```

### Animations
- Les personnages sont dessinés sur la base du style "pixel art"
- Les chiens courent dans une ruelle sombre

## Configuration
à définir*
```
