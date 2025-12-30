# 🎬 Guide Rapide - Présentation El Bazar

## 📄 Document Principal
Le script complet de présentation se trouve dans **[PRESENTATION_SCRIPT.md](./PRESENTATION_SCRIPT.md)**

## ⚡ Accès Rapide

### Pour une présentation orale
➡️ Consultez les sections avec le symbole 🎯 **"Script de présentation"**

### Pour montrer le code
➡️ Consultez les sections avec le symbole 💻 **"Code correspondant"**

### Pour filmer une démo
➡️ Consultez les sections avec le symbole 📹 **"À montrer dans la vidéo"**

---

## 📋 Structure du Script (1298 lignes)

### 1. Introduction (Lignes 1-70)
- Vue d'ensemble de la plateforme
- Architecture technique
- Technologies utilisées

### 2. Architecture Technique (Lignes 71-150)
- Stack Frontend : React + TypeScript + Vite
- Stack Backend : Node.js + Express + Prisma
- Schéma de base de données

### 3. Système d'Authentification (Lignes 151-280)
- Inscription client/vendeur
- Connexion avec JWT
- Middleware de sécurité
- **Code:** `/frontend/src/components/RegisterForm.tsx`, `/backend/src/controllers/authController.js`

### 4. Fonctionnalités Acheteur (Lignes 281-570)
- Page d'accueil (liste vendeurs)
- Navigation produits avec filtres
- Gestion du panier
- Passage de commande
- Suivi des commandes
- **Code:** `/frontend/src/pages/ProductsPage.tsx`, `/frontend/App.tsx`

### 5. Fonctionnalités Vendeur (Lignes 571-950)
- Dashboard avec statistiques
- CRUD complet des produits
- Gestion des commandes
- Profil de boutique
- **Code:** `/frontend/src/pages/SellerDashboard.tsx`, `/frontend/src/components/ProductForm.tsx`

### 6. Fonctionnalités Avancées (Lignes 951-1150)
- Chatbot IA
- Hooks React (useState, useEffect, useCallback, useMemo, useContext)
- Composants UI Shadcn
- Gestion d'images Base64
- Responsive design
- **Code:** `/frontend/App.tsx`, `/frontend/src/pages/ChatBotPage.tsx`

### 7. Guide Vidéo Détaillé (Lignes 1151-1250)
- Plan de tournage minute par minute (12 minutes)
- Conseils de préparation
- Éléments à mettre en avant
- Outils recommandés

### 8. Tableau Récapitulatif (Lignes 1251-1298)
- Mapping Fonctionnalité → Code → Vidéo
- Points clés à mentionner
- Ressources additionnelles

---

## 🎥 Plan Vidéo en 6 Parties

| Partie | Durée | Contenu Principal |
|--------|-------|-------------------|
| 1. Introduction | 1 min | Architecture générale |
| 2. Authentification | 2 min | Inscription/Connexion |
| 3. Expérience Acheteur | 3 min | Produits, panier, commandes |
| 4. Dashboard Vendeur | 4 min | Statistiques, CRUD, gestion |
| 5. Fonctionnalités Avancées | 2 min | Chatbot, hooks, responsive |
| 6. Architecture Technique | 1 min | Code backend/frontend |
| **Total** | **~12 min** | Présentation complète |

---

## 🔑 Fichiers Clés à Montrer

### Frontend
```
/frontend/
├── App.tsx                          ⭐ Point d'entrée, Context, Hooks
├── src/
│   ├── pages/
│   │   ├── HomePage.tsx             ⭐ Page d'accueil vendeurs
│   │   ├── ProductsPage.tsx         ⭐ Liste produits avec filtres
│   │   ├── SellerDashboard.tsx      ⭐ Dashboard vendeur complet
│   │   ├── MyOrdersPage.tsx         📦 Commandes acheteur
│   │   ├── StoreProfilePage.tsx     🏪 Profil boutique
│   │   └── ChatBotPage.tsx          🤖 Chatbot IA
│   ├── components/
│   │   ├── Header.tsx               🔝 Navigation
│   │   ├── ProductCard.tsx          📦 Carte produit
│   │   ├── ProductForm.tsx          ✏️ Formulaire produit (CRUD)
│   │   ├── RegisterForm.tsx         🔐 Inscription
│   │   ├── Login.tsx                🔐 Connexion
│   │   └── ui/                      🎨 Composants Shadcn
│   └── services/
│       ├── authService.ts           🔐 API Auth
│       ├── productService.ts        📦 API Produits
│       └── orderService.ts          🛒 API Commandes
```

### Backend
```
/backend/
├── src/
│   ├── server.js                    ⭐ Point d'entrée serveur
│   ├── controllers/
│   │   ├── authController.js        🔐 Logique authentification
│   │   ├── prismaProductController.js 📦 Logique produits
│   │   └── orderController.js       🛒 Logique commandes
│   ├── routes/
│   │   ├── authRoutes.js            🔐 Routes auth
│   │   ├── productRoutes.js         📦 Routes produits
│   │   └── orderRoutes.js           🛒 Routes commandes
│   ├── middleware/
│   │   └── auth.js                  🔒 JWT validation
│   └── models/
│       └── db.js                    💾 Config Prisma
├── prisma/
│   ├── schema.prisma                ⭐ Schéma base de données
│   └── seed.js                      🌱 Données de test
└── chatbot.py                       🤖 Chatbot Python
```

---

## 📊 Checklist de Présentation

### Préparation
- [ ] Backend démarré (`cd backend && npm start`)
- [ ] Frontend démarré (`cd frontend && npm run dev`)
- [ ] Base de données peuplée (seed)
- [ ] Comptes de test prêts
- [ ] Images de test prêtes
- [ ] Enregistreur d'écran configuré

### Démonstration
- [ ] Introduction et architecture (1 min)
- [ ] Inscription vendeur (30s)
- [ ] Dashboard vendeur + CRUD produits (2 min)
- [ ] Connexion acheteur (15s)
- [ ] Navigation produits + filtres (1 min)
- [ ] Panier + commande (1 min)
- [ ] Gestion commandes vendeur (45s)
- [ ] Chatbot (30s)
- [ ] Code : hooks et architecture (1 min)
- [ ] Responsive design (20s)
- [ ] Conclusion (15s)

### Points Techniques à Mentionner
- [ ] React 18 + TypeScript
- [ ] Hooks avancés (useCallback, useMemo, useContext)
- [ ] Prisma ORM + SQLite
- [ ] JWT Authentication
- [ ] Shadcn/ui composants
- [ ] Tailwind CSS
- [ ] Base64 images
- [ ] Architecture frontend/backend séparée

---

## 💡 Conseils

### Pour l'oral
1. Parlez clairement et pas trop vite
2. Montrez d'abord l'interface, puis le code
3. Expliquez la logique, pas seulement la syntaxe
4. Mettez en avant les bonnes pratiques

### Pour la vidéo
1. Résolution 1080p minimum
2. Curseur bien visible
3. Zoom sur les détails importants
4. Transitions fluides
5. Pauses après actions importantes

### Pour le code
1. Montrez les fichiers principaux
2. Surlignez les lignes importantes
3. Expliquez la structure des dossiers
4. Mentionnez les patterns utilisés

---

## 🚀 Démarrage Rapide

```bash
# Terminal 1 - Backend
cd backend
npm install
npx prisma generate
npx prisma db push
node prisma/seed.js
npm start

# Terminal 2 - Frontend
cd frontend
npm install
npm run dev

# Navigateur
http://localhost:3000
```

### Comptes de Test
**Acheteur:**
- Email: `buyer@example.com`
- Mot de passe: `password123`

**Vendeur:**
- Email: `seller@example.com`
- Mot de passe: `password123`

---

## 📚 Ressources Complémentaires

- **[README.md](./README.md)** - Documentation générale
- **[USER_GUIDE.md](./USER_GUIDE.md)** - Guide utilisateur détaillé
- **[IMPLEMENTATION_SUMMARY.md](./IMPLEMENTATION_SUMMARY.md)** - Résumé technique
- **[DATABASE_FIX_SUMMARY.md](./DATABASE_FIX_SUMMARY.md)** - Architecture BDD
- **[PRESENTATION_SCRIPT.md](./PRESENTATION_SCRIPT.md)** - Script complet ⭐

---

**Bonne présentation ! 🎉**
