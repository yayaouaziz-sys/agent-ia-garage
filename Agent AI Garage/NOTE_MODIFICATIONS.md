# Agent IA Garage - Notes de Modifications

## Structure des fichiers

```
Agent AI Garage/
├── index.html          <- Fichier principal
└── assets/
    ├── favicon.png     <- Logo ecran accueil (120x120px)
    ├── logo-center.png <- Logo header (40px hauteur)
    └── logo-header.png <- Favicon navigateur
```

---

## Modifications apportees au code

### 1. Images adaptees
- **Header**: `height: 40px` avec `object-fit: contain`
- **Accueil**: `120x120px` avec `object-fit: contain`
- Les images gardent leurs proportions automatiquement

### 2. Responsive Mobile
Le chatbot s'adapte a tous les ecrans:

| Ecran | Comportement |
|-------|--------------|
| < 380px | Petits telephones - tailles reduites |
| < 480px | Plein ecran, pas de bordures |
| 481-768px | Tablettes - 85% hauteur |
| > 769px | Desktop - taille fixe 650px |
| Paysage | Optimise pour ecran horizontal |

### 3. Fix hauteur mobile
```javascript
function setVH() {
    let vh = window.innerHeight * 0.01;
    document.documentElement.style.setProperty('--vh', `${vh}px`);
}
```
Corrige le probleme de la barre d'adresse sur mobile.

### 4. Optimisations tactiles
- `-webkit-tap-highlight-color: transparent` - Pas de flash au tap
- `font-size: 16px` sur input - Empeche le zoom iOS
- `env(safe-area-inset-bottom)` - Support iPhone avec encoche

---

## CSS Responsive complet

```css
/* Petits telephones */
@media screen and (max-width: 380px) {
    .chat-container { height: 95vh; border-radius: 15px; }
    .chat-header img { height: 35px; }
    .welcome-screen img { width: 100px; height: 100px; }
}

/* Telephones standards */
@media screen and (max-width: 480px) {
    body { padding: 0; }
    .chat-container { height: 100vh; border-radius: 0; }
}

/* Tablettes */
@media screen and (min-width: 481px) and (max-width: 768px) {
    .chat-container { max-width: 450px; height: 85vh; }
}

/* Desktop */
@media screen and (min-width: 769px) {
    .chat-container { max-width: 500px; height: 650px; }
    .welcome-screen img { width: 140px; height: 140px; }
}

/* Mode paysage */
@media screen and (max-height: 500px) and (orientation: landscape) {
    .welcome-screen img { width: 80px; height: 80px; }
}
```

---

## Deploiement GitHub Pages

1. Creer repo GitHub
2. Ajouter les fichiers:
   - `index.html`
   - `assets/favicon.png`
   - `assets/logo-center.png`
3. Settings > Pages > Source: main branch
4. URL: `https://username.github.io/repo-name/`

---

## Webhook n8n

URL: `https://n8n.srv1260361.hstgr.cloud/webhook/garage-agent`

Donnees envoyees:
```json
{
    "message": "texte utilisateur",
    "session_id": "session_xxx",
    "session_state": {},
    "garage_id": "GARAGE_001"
}
```
