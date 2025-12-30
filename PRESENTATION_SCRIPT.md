# 🎬 El Bazar - Script de Présentation et Guide Vidéo

## 📋 Table des matières
1. [Introduction](#introduction)
2. [Architecture technique](#architecture-technique)
3. [Système d'authentification](#système-dauthentification)
4. [Fonctionnalités Acheteur](#fonctionnalités-acheteur)
5. [Fonctionnalités Vendeur](#fonctionnalités-vendeur)
6. [Fonctionnalités Avancées](#fonctionnalités-avancées)
7. [Guide Vidéo Parallèle](#guide-vidéo-parallèle)

---

## 🎯 Introduction

### Script de présentation :
> "Bienvenue dans El Bazar, une plateforme e-commerce moderne construite avec les dernières technologies web. El Bazar connecte les acheteurs locaux et les vendeurs dans un marketplace digital unifié."

### Code correspondant :
**Fichier principal :** `/frontend/App.tsx`
- **Lignes 1-10 :** Imports des pages et contextes
- **Lignes 62-260 :** Composant principal App avec gestion d'état

**Composants clés :**
```typescript
// CartContext - Gestion globale du panier (lignes 23-41)
interface CartContextType {
  cart: CartItem[];
  addToCart: (item: Omit<CartItem, 'quantity'>, quantity?: number) => void;
  removeFromCart: (id: string | number) => void;
  clearCart: () => void;
  cartTotal: number;
  cartItemsCount: number;
  showToast: (message: string, type?: 'success' | 'error' | 'info' | 'warning') => void;
}
```

### 📹 À montrer dans la vidéo :
- [ ] Page d'accueil avec logo El Bazar
- [ ] Navigation fluide entre les pages
- [ ] Interface responsive et moderne
- [ ] Survol rapide des principales sections

**Durée : 30 secondes**

---

## 🏗️ Architecture technique

### Script de présentation :
> "L'application suit une architecture moderne avec séparation claire entre frontend et backend. Le frontend utilise React 18 avec TypeScript, tandis que le backend repose sur Node.js, Express et Prisma ORM avec SQLite."

### Code correspondant :

**Frontend - Stack technologique :**
- **Framework :** React 18 + TypeScript
- **Build Tool :** Vite (`/frontend/vite.config.ts`)
- **Styling :** Tailwind CSS (`/frontend/index.css`)
- **UI Components :** Shadcn/ui (`/frontend/src/components/ui/`)
- **Icons :** Lucide React

**Fichier :** `/frontend/package.json`
```json
{
  "dependencies": {
    "react": "^18.3.1",
    "lucide-react": "^0.462.0",
    "@radix-ui/react-*": "Composants UI"
  }
}
```

**Backend - Stack technologique :**
- **Runtime :** Node.js
- **Framework :** Express.js
- **ORM :** Prisma (`/backend/prisma/schema.prisma`)
- **Database :** SQLite (dev.db)
- **Authentication :** JWT + bcryptjs

**Fichier :** `/backend/src/server.js` (lignes 1-30)
```javascript
const express = require('express');
const cors = require('cors');
const authRoutes = require('./routes/authRoutes');
const productRoutes = require('./routes/productRoutes');
const orderRoutes = require('./routes/orderRoutes');
```

**Base de données - Schéma Prisma :**
**Fichier :** `/backend/prisma/schema.prisma`
- **User Model :** Lignes 31-45 (Utilisateurs et vendeurs)
- **Product Model :** Lignes 14-29 (Produits)
- **Order Model :** Lignes 47-57 (Commandes)
- **OrderItem Model :** Lignes 59-69 (Articles commandés)
- **Contact Model :** Lignes 71-79 (Messages de contact)

### 📹 À montrer dans la vidéo :
- [ ] Ouvrir l'éditeur de code montrant la structure du projet
- [ ] Montrer `/frontend/src/` et `/backend/src/`
- [ ] Ouvrir rapidement `schema.prisma` pour montrer les modèles
- [ ] Montrer le terminal avec backend et frontend running

**Durée : 45 secondes**

---

## 🔐 Système d'authentification

### Script de présentation :
> "El Bazar offre un système d'authentification complet avec inscription et connexion pour deux types d'utilisateurs : les acheteurs (clients) et les vendeurs. L'authentification utilise JWT pour sécuriser les sessions."

### Code correspondant :

**Composant d'inscription :**
**Fichier :** `/frontend/src/components/RegisterForm.tsx`
- **Lignes 1-50 :** Interface et types
- **Lignes 80-150 :** Formulaire avec sélection de rôle (client/vendeur)
- **Logique :** Différenciation automatique des champs selon le rôle

**Composant de connexion :**
**Fichier :** `/frontend/src/components/Login.tsx`
- **Lignes 1-30 :** État et gestion du formulaire
- **Lignes 40-80 :** Soumission et validation

**Backend - Contrôleur d'authentification :**
**Fichier :** `/backend/src/controllers/authController.js`

**Fonction register (lignes ~10-80) :**
```javascript
// Hachage du mot de passe avec bcrypt
const hashedPassword = await bcrypt.hash(password, 10);

// Création de l'utilisateur dans Prisma
const user = await prisma.user.create({
  data: { email, name, password: hashedPassword, role, ... }
});

// Génération du token JWT
const token = jwt.sign({ id: user.id, role: user.role }, JWT_SECRET);
```

**Fonction login (lignes ~90-140) :**
```javascript
// Vérification de l'utilisateur
const user = await prisma.user.findUnique({ where: { email } });

// Validation du mot de passe
const validPassword = await bcrypt.compare(password, user.password);

// Génération du token
const token = jwt.sign({ id: user.id, role: user.role }, JWT_SECRET);
```

**Middleware d'authentification :**
**Fichier :** `/backend/src/middleware/auth.js`
```javascript
// Vérification du token JWT
const token = req.headers.authorization?.split(' ')[1];
const decoded = jwt.verify(token, JWT_SECRET);
req.user = decoded;
```

### 📹 À montrer dans la vidéo :
- [ ] Cliquer sur "Connexion" dans le header
- [ ] Montrer le formulaire de connexion
- [ ] Passer à l'onglet "S'inscrire"
- [ ] Montrer la sélection de rôle (Client vs Vendeur)
- [ ] Pour Client : montrer les champs (nom, email, téléphone, mot de passe)
- [ ] Pour Vendeur : montrer les champs supplémentaires (nom boutique, adresse, logo)
- [ ] Effectuer une inscription vendeur complète
- [ ] Montrer la redirection automatique vers le dashboard vendeur

**Durée : 1 minute 30 secondes**

---

## 🛒 Fonctionnalités Acheteur

### Script de présentation :
> "Les acheteurs ont accès à une expérience complète d'e-commerce : navigation des produits avec filtres avancés, gestion du panier d'achat, passage de commandes et suivi."

### 1. Page d'accueil - Liste des vendeurs

**Fichier :** `/frontend/src/pages/HomePage.tsx`

**Code clé :**
```typescript
// Chargement des vendeurs depuis l'API (lignes 45-70)
const fetchSellers = async () => {
  const [sellersRes, productsRes] = await Promise.all([
    fetch('http://localhost:5000/api/auth/sellers'),
    fetch('http://localhost:5000/api/products')
  ]);
  
  // Calcul du nombre de produits par vendeur
  const counts = productsData.reduce((acc, product) => {
    acc[product.sellerId] = (acc[product.sellerId] || 0) + 1;
    return acc;
  }, {});
};
```

**Composant SellerCard :**
**Fichier :** `/frontend/src/components/SellerCard.tsx`
- Affiche : Logo, nom boutique, nombre de produits
- Action : Clic pour voir le profil du vendeur

### 📹 À montrer dans la vidéo :
- [ ] Se connecter en tant qu'acheteur (buyer@example.com)
- [ ] Montrer la page d'accueil avec la grille de vendeurs
- [ ] Montrer les cartes vendeurs avec logos et nombres de produits
- [ ] Cliquer sur un vendeur pour voir son profil

**Durée : 30 secondes**

---

### 2. Page Produits - Navigation et filtrage

**Fichier :** `/frontend/src/pages/ProductsPage.tsx`

**Code clé :**
```typescript
// Chargement des produits (lignes 39-50)
const loadBackendProducts = async () => {
  const data = await getProducts();
  setBackendProducts(data);
};

// Filtrage par catégorie (lignes 70-90)
const filteredProducts = backendProducts.filter(product => 
  selectedCategory === 'all' || product.category === selectedCategory
);

// Tri des produits (lignes 100-120)
const sortedProducts = [...filteredProducts].sort((a, b) => {
  if (sortBy === 'price-asc') return a.price - b.price;
  if (sortBy === 'price-desc') return b.price - a.price;
  if (sortBy === 'rating') return b.rating - a.rating;
  return 0;
});
```

**Service API :**
**Fichier :** `/frontend/src/services/productService.ts`
```typescript
export const getProducts = async () => {
  const response = await fetch(`${API_URL}/products`, {
    headers: { 'Authorization': `Bearer ${token}` }
  });
  return response.json();
};
```

**Composant CategoryFilter :**
**Fichier :** `/frontend/src/components/CategoryFilter.tsx`
- Catégories disponibles : Meubles, Électronique, Mode, Alimentation, Beauté, Sports, Livres, Autres
- Sélection visuelle avec badges

**Composant ProductCard :**
**Fichier :** `/frontend/src/components/ProductCard.tsx`
- Affiche : Image, nom, prix, note, stock
- Actions : Ajouter au panier, favoris, partager
- Gestion des réductions (badge promo)

### 📹 À montrer dans la vidéo :
- [ ] Cliquer sur "Produits" dans le menu
- [ ] Montrer tous les produits (de tous les vendeurs)
- [ ] Utiliser le filtre de catégorie (ex: Électronique)
- [ ] Montrer le tri par prix (croissant/décroissant)
- [ ] Montrer le tri par note
- [ ] Basculer entre vue grille et liste
- [ ] Survol d'un produit pour montrer les actions (favoris, partage)

**Durée : 1 minute**

---

### 3. Gestion du panier

**Fichier :** `/frontend/App.tsx`

**Context du panier (lignes 23-41) :**
```typescript
interface CartContextType {
  cart: CartItem[];
  addToCart: (item, quantity) => void;
  removeFromCart: (id) => void;
  clearCart: () => void;
  cartTotal: number;
  cartItemsCount: number;
}
```

**Logique d'ajout au panier (lignes 135-147) :**
```typescript
const addToCart = useCallback((item, quantity = 1) => {
  setCart((prevCart) => {
    const existingItem = prevCart.find((cartItem) => cartItem.id === item.id);
    if (existingItem) {
      // Augmenter la quantité si déjà dans le panier
      return prevCart.map((cartItem) =>
        cartItem.id === item.id
          ? { ...cartItem, quantity: cartItem.quantity + quantity }
          : cartItem
      );
    }
    // Ajouter nouveau produit
    return [...prevCart, { ...item, quantity }];
  });
}, []);
```

**Persistance localStorage (lignes 43-60) :**
```typescript
// Chargement depuis localStorage au démarrage
const loadCart = (): CartItem[] => {
  const savedCart = localStorage.getItem('cart');
  return savedCart ? JSON.parse(savedCart) : [];
};

// Sauvegarde automatique à chaque modification
useEffect(() => {
  saveCart(cart);
}, [cart]);
```

**Composant Header - Icône panier :**
**Fichier :** `/frontend/src/components/Header.tsx`
- Badge avec nombre d'articles
- Modal panier au clic

### 📹 À montrer dans la vidéo :
- [ ] Ajouter plusieurs produits au panier
- [ ] Montrer le badge panier s'incrémenter
- [ ] Cliquer sur l'icône panier
- [ ] Montrer la modal avec liste des produits
- [ ] Modifier les quantités
- [ ] Supprimer un article
- [ ] Montrer le total calculé
- [ ] Fermer et rouvrir : persistance des données

**Durée : 1 minute 15 secondes**

---

### 4. Passage de commande

**Service de commande :**
**Fichier :** `/frontend/src/services/orderService.ts`
```typescript
export const createOrder = async (orderData) => {
  const response = await fetch(`${API_URL}/orders`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${token}`
    },
    body: JSON.stringify(orderData)
  });
  return response.json();
};
```

**Backend - Contrôleur de commande :**
**Fichier :** `/backend/src/controllers/orderController.js`

**Fonction createOrder :**
```javascript
// Création de la commande avec items
const order = await prisma.order.create({
  data: {
    userId: req.user.id,
    sellerId: items[0].sellerId,
    total: orderTotal,
    status: 'pending',
    items: {
      create: items.map(item => ({
        productId: item.id,
        name: item.name,
        price: item.price,
        quantity: item.quantity,
        image: item.image
      }))
    }
  },
  include: { items: true }
});
```

### 📹 À montrer dans la vidéo :
- [ ] Dans le panier, cliquer "Commander"
- [ ] Montrer la confirmation de commande
- [ ] Montrer que le panier est vidé
- [ ] Aller dans "Mes Commandes"
- [ ] Montrer la commande créée avec statut "En attente"

**Durée : 45 secondes**

---

### 5. Suivi des commandes

**Fichier :** `/frontend/src/pages/MyOrdersPage.tsx`

**Code clé :**
```typescript
// Chargement des commandes utilisateur
const loadOrders = async () => {
  const data = await getUserOrders();
  setOrders(data);
};

// Affichage avec statut et items
orders.map(order => (
  <OrderCard 
    order={order}
    items={order.items}
    status={order.status}  // pending, confirmed, shipped, delivered
    total={order.total}
  />
))
```

**Backend - Route :**
**Fichier :** `/backend/src/routes/orderRoutes.js`
```javascript
router.get('/', authenticateToken, async (req, res) => {
  const orders = await prisma.order.findMany({
    where: { userId: req.user.id },
    include: { items: true, seller: true },
    orderBy: { createdAt: 'desc' }
  });
});
```

### 📹 À montrer dans la vidéo :
- [ ] Naviguer vers "Mes Commandes"
- [ ] Montrer la liste des commandes
- [ ] Montrer les détails d'une commande (items, total, statut)
- [ ] Montrer les différents statuts possibles

**Durée : 30 secondes**

---

## 🏪 Fonctionnalités Vendeur

### Script de présentation :
> "Les vendeurs disposent d'un dashboard complet pour gérer leur boutique : statistiques en temps réel, gestion des produits (CRUD complet), suivi des commandes et personnalisation du profil."

### 1. Dashboard vendeur - Vue d'ensemble

**Fichier :** `/frontend/src/pages/SellerDashboard.tsx`

**Chargement des données (lignes 34-49) :**
```typescript
const loadData = async () => {
  const [productsData, ordersData] = await Promise.all([
    getSellerProducts(),
    getSellerOrders()
  ]);
  setProducts(productsData);
  setOrders(ordersData);
};
```

**Calcul des statistiques (lignes 80-120) :**
```typescript
// Revenu total
const totalRevenue = orders
  .filter(order => order.status !== 'cancelled')
  .reduce((sum, order) => sum + order.total, 0);

// Nombre de commandes
const ordersCount = orders.filter(order => order.status !== 'cancelled').length;

// Nombre de produits actifs
const activeProducts = products.filter(p => p.stock > 0).length;

// Taux de croissance (exemple)
const growthRate = 12.5; // Basé sur les commandes du mois précédent
```

**Composant StatCard :**
**Fichier :** `/frontend/src/components/StatCard.tsx`
- Affiche : Valeur, titre, icône, tendance
- Variants : success, warning, info

### 📹 À montrer dans la vidéo :
- [ ] Se connecter en tant que vendeur (seller@example.com)
- [ ] Montrer la redirection automatique vers le dashboard
- [ ] Montrer les 3 cartes de statistiques en haut :
  - Revenu total
  - Nombre de commandes
  - Produits actifs
- [ ] Montrer les icônes et les pourcentages de croissance

**Durée : 30 secondes**

---

### 2. Gestion des produits (CRUD)

**a) Création de produit**

**Composant ProductForm :**
**Fichier :** `/frontend/src/components/ProductForm.tsx`

**Code clé :**
```typescript
// Formulaire avec upload d'image
const [formData, setFormData] = useState({
  name: '',
  price: 0,
  category: '',
  stock: 0,
  description: '',
  discount: 0,
  image: ''  // Base64 après upload
});

// Gestion upload image
const handleImageChange = (e) => {
  const file = e.target.files?.[0];
  if (file) {
    const reader = new FileReader();
    reader.onloadend = () => {
      setFormData({ ...formData, image: reader.result as string });
    };
    reader.readAsDataURL(file);
  }
};

// Soumission
const handleSubmit = async () => {
  if (isEditing) {
    await updateProduct(product.id, formData);
  } else {
    await createProduct(formData);
  }
};
```

**Service API :**
**Fichier :** `/frontend/src/services/productService.ts`
```typescript
export const createProduct = async (productData) => {
  const response = await fetch(`${API_URL}/products`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${token}`
    },
    body: JSON.stringify(productData)
  });
};
```

**Backend - Contrôleur :**
**Fichier :** `/backend/src/controllers/prismaProductController.js`
```javascript
const createProduct = async (req, res) => {
  const { name, price, category, stock, description, discount, image } = req.body;
  
  const product = await prisma.product.create({
    data: {
      name,
      price: parseFloat(price),
      category,
      categoryId: category.toLowerCase(),
      stock: parseInt(stock),
      description,
      discount: discount ? parseInt(discount) : null,
      image,
      sellerId: req.user.id,
      rating: 0
    }
  });
};
```

### 📹 À montrer dans la vidéo :
- [ ] Dans le dashboard, cliquer "+ Ajouter Produit"
- [ ] Montrer le formulaire modal
- [ ] Remplir tous les champs :
  - Nom du produit
  - Prix
  - Catégorie (dropdown)
  - Stock
  - Description
  - Réduction (optionnel)
  - Upload d'image (montrer le preview)
- [ ] Cliquer "Ajouter"
- [ ] Montrer le produit apparaître dans le tableau

**Durée : 1 minute**

---

**b) Liste et affichage des produits**

**Code clé (SellerDashboard.tsx, lignes 150-250) :**
```typescript
<Table>
  <TableHeader>
    <TableRow>
      <TableHead>Image</TableHead>
      <TableHead>Produit</TableHead>
      <TableHead>Prix</TableHead>
      <TableHead>Stock</TableHead>
      <TableHead>Catégorie</TableHead>
      <TableHead>Actions</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    {products.map(product => (
      <TableRow key={product.id}>
        <TableCell>
          <img src={product.image} className="w-12 h-12" />
        </TableCell>
        <TableCell>{product.name}</TableCell>
        <TableCell>{formatTND(product.price)}</TableCell>
        <TableCell>
          <Badge variant={product.stock > 0 ? 'default' : 'destructive'}>
            {product.stock} en stock
          </Badge>
        </TableCell>
        <TableCell>{product.category}</TableCell>
        <TableCell>
          <Button onClick={() => handleEdit(product)}>
            <Pencil className="h-4 w-4" />
          </Button>
          <Button onClick={() => handleDelete(product.id)}>
            <Trash2 className="h-4 w-4" />
          </Button>
        </TableCell>
      </TableRow>
    ))}
  </TableBody>
</Table>
```

### 📹 À montrer dans la vidéo :
- [ ] Montrer le tableau de produits
- [ ] Souligner les colonnes importantes
- [ ] Montrer les badges de stock (vert si en stock, rouge si épuisé)
- [ ] Montrer les icônes d'actions (modifier, supprimer)

**Durée : 20 secondes**

---

**c) Modification de produit**

**Code clé :**
```typescript
const handleEdit = (product) => {
  setEditingProduct(product);
  setShowProductForm(true);
};

// ProductForm reçoit le produit existant
<ProductForm
  isOpen={showProductForm}
  onClose={() => {
    setShowProductForm(false);
    setEditingProduct(null);
  }}
  product={editingProduct}  // Pré-rempli si modification
  onProductAdded={loadData}
/>
```

**Service API :**
```typescript
export const updateProduct = async (id, productData) => {
  const response = await fetch(`${API_URL}/products/${id}`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${token}`
    },
    body: JSON.stringify(productData)
  });
};
```

### 📹 À montrer dans la vidéo :
- [ ] Cliquer sur l'icône "Modifier" (crayon) d'un produit
- [ ] Montrer le formulaire pré-rempli
- [ ] Modifier un champ (ex: le prix ou le stock)
- [ ] Sauvegarder
- [ ] Montrer le produit mis à jour dans le tableau

**Durée : 30 secondes**

---

**d) Suppression de produit**

**Code clé :**
```typescript
const handleDelete = async (id) => {
  if (window.confirm('Êtes-vous sûr de vouloir supprimer ce produit ?')) {
    try {
      await deleteProduct(id);
      loadData();  // Recharger la liste
    } catch (error) {
      console.error('Erreur lors de la suppression:', error);
    }
  }
};
```

**Backend :**
```javascript
const deleteProduct = async (req, res) => {
  await prisma.product.delete({
    where: { 
      id: parseInt(req.params.id),
      sellerId: req.user.id  // Sécurité : seul le propriétaire peut supprimer
    }
  });
};
```

### 📹 À montrer dans la vidéo :
- [ ] Cliquer sur l'icône "Supprimer" (poubelle)
- [ ] Montrer la confirmation
- [ ] Confirmer
- [ ] Montrer le produit disparaître du tableau

**Durée : 15 secondes**

---

### 3. Gestion des commandes vendeur

**Fichier :** `/frontend/src/pages/SellerDashboard.tsx`

**Code clé (lignes 300-400) :**
```typescript
// Filtrage des commandes
const filteredOrders = orderFilter === 'all' 
  ? orders 
  : orders.filter(order => order.status === orderFilter);

// Mise à jour du statut
const handleUpdateStatus = async (orderId, newStatus) => {
  try {
    await updateOrderStatus(orderId, newStatus);
    loadData();  // Recharger
  } catch (error) {
    console.error('Erreur mise à jour statut:', error);
  }
};

// Affichage
<Table>
  <TableBody>
    {filteredOrders.map(order => (
      <TableRow key={order.id}>
        <TableCell>#{order.id}</TableCell>
        <TableCell>{order.user.name}</TableCell>
        <TableCell>{formatTND(order.total)}</TableCell>
        <TableCell>
          <Badge variant={getStatusVariant(order.status)}>
            {getStatusLabel(order.status)}
          </Badge>
        </TableCell>
        <TableCell>
          <select 
            value={order.status}
            onChange={(e) => handleUpdateStatus(order.id, e.target.value)}
          >
            <option value="pending">En attente</option>
            <option value="confirmed">Confirmée</option>
            <option value="shipped">Expédiée</option>
            <option value="delivered">Livrée</option>
            <option value="cancelled">Annulée</option>
          </select>
        </TableCell>
      </TableRow>
    ))}
  </TableBody>
</Table>
```

**Backend - Service de commande :**
**Fichier :** `/backend/src/controllers/orderController.js`
```javascript
// Récupération des commandes du vendeur
const getSellerOrders = async (req, res) => {
  const orders = await prisma.order.findMany({
    where: { sellerId: req.user.id },
    include: { items: true, user: true },
    orderBy: { createdAt: 'desc' }
  });
};

// Mise à jour du statut
const updateOrderStatus = async (req, res) => {
  const order = await prisma.order.update({
    where: { 
      id: parseInt(req.params.id),
      sellerId: req.user.id  // Sécurité
    },
    data: { status: req.body.status }
  });
};
```

### 📹 À montrer dans la vidéo :
- [ ] Scroller vers la section "Commandes reçues"
- [ ] Montrer le tableau des commandes
- [ ] Montrer les filtres de statut
- [ ] Cliquer sur une commande pour voir les détails (items)
- [ ] Modifier le statut d'une commande (ex: pending → confirmed)
- [ ] Montrer le badge de statut changer de couleur

**Durée : 45 secondes**

---

### 4. Profil de boutique (Store Profile)

**Fichier :** `/frontend/src/pages/StoreProfilePage.tsx`

**Code clé :**
```typescript
// Chargement du profil vendeur
const loadStoreProfile = async () => {
  const response = await fetch(`${API_URL}/auth/sellers`);
  const sellers = await response.json();
  const seller = sellers.find(s => s.id == sellerId);
  setStore(seller);
  
  // Charger les produits du vendeur
  const allProducts = await getProducts();
  const sellerProducts = allProducts.filter(p => p.sellerId == sellerId);
  setProducts(sellerProducts);
};

// Affichage
<div className="store-header">
  <img src={store.storePhoto} alt={store.storeName} />
  <h1>{store.storeName}</h1>
  <p>{store.address}</p>
  <p>{store.phone}</p>
</div>

<div className="products-grid">
  {products.map(product => (
    <ProductCard product={product} />
  ))}
</div>
```

### 📹 À montrer dans la vidéo :
- [ ] En tant qu'acheteur, cliquer sur un vendeur depuis la page d'accueil
- [ ] Montrer le profil de la boutique :
  - Logo de la boutique
  - Nom de la boutique
  - Adresse
  - Téléphone
- [ ] Montrer les produits de ce vendeur uniquement
- [ ] Montrer qu'on peut ajouter au panier depuis ce profil

**Durée : 30 secondes**

---

## ⚡ Fonctionnalités Avancées

### 1. Chatbot (Intelligence artificielle)

**Fichier Backend :** `/backend/chatbot.py`
- Chatbot Python avec traitement du langage naturel
- Répond aux questions sur les produits, commandes, etc.

**Fichier Frontend :** `/frontend/src/pages/ChatBotPage.tsx`

**Code clé :**
```typescript
const sendMessage = async (message: string) => {
  setMessages([...messages, { text: message, sender: 'user' }]);
  
  // Appel à l'API du chatbot
  const response = await fetch('http://localhost:5000/api/chatbot', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ message })
  });
  
  const data = await response.json();
  setMessages([...messages, 
    { text: message, sender: 'user' },
    { text: data.response, sender: 'bot' }
  ]);
};
```

### 📹 À montrer dans la vidéo :
- [ ] Cliquer sur "Chatbot" dans le menu
- [ ] Montrer l'interface de chat
- [ ] Poser une question (ex: "Quels produits électroniques avez-vous ?")
- [ ] Montrer la réponse du bot
- [ ] Poser 2-3 questions différentes

**Durée : 45 secondes**

---

### 2. Hooks React avancés

**Fichier :** `/frontend/App.tsx`

**a) useState - Gestion d'état :**
```typescript
// Exemples (lignes 65-71)
const [userRole, setUserRole] = useState<UserRole>(null);
const [isLoggedIn, setIsLoggedIn] = useState(false);
const [currentPage, setCurrentPage] = useState<CurrentPage>('home');
const [cart, setCart] = useState<CartItem[]>(loadCart);
```

**b) useEffect - Effets de bord :**
```typescript
// Auto-login au chargement (lignes 76-96)
useEffect(() => {
  const checkAuth = async () => {
    const user = getCurrentUser();
    if (user) {
      setUserRole(user.role);
      setIsLoggedIn(true);
    }
  };
  checkAuth();
}, []);

// Sauvegarde panier (lignes 99-101)
useEffect(() => {
  saveCart(cart);
}, [cart]);
```

**c) useCallback - Mémorisation de fonctions :**
```typescript
// Optimisation performance (lignes 135-155)
const addToCart = useCallback((item, quantity = 1) => {
  setCart((prevCart) => {
    // Logique d'ajout...
  });
}, []);

const removeFromCart = useCallback((id) => {
  setCart((prevCart) => prevCart.filter((item) => item.id !== id));
}, []);
```

**d) useMemo - Mémorisation de valeurs :**
```typescript
// Calculs optimisés (lignes 158-164)
const cartTotal = useMemo(() => {
  return cart.reduce((total, item) => total + item.price * item.quantity, 0);
}, [cart]);

const cartItemsCount = useMemo(() => {
  return cart.reduce((count, item) => count + item.quantity, 0);
}, [cart]);
```

**e) useContext - Partage d'état global :**
```typescript
// Context pour le panier (lignes 33-41)
export const CartContext = createContext<CartContextType>({...});

// Utilisation dans les composants
const { addToCart, cart, cartTotal } = useContext(CartContext);
```

### 📹 À montrer dans la vidéo :
- [ ] Ouvrir le code de App.tsx dans l'éditeur
- [ ] Montrer rapidement les hooks avec surlignage :
  - useState pour l'état
  - useEffect pour le cycle de vie
  - useCallback pour les callbacks
  - useMemo pour les calculs
  - useContext pour le partage
- [ ] Expliquer : "Ces hooks permettent optimisation et réactivité"

**Durée : 30 secondes**

---

### 3. Composants UI réutilisables (Shadcn/ui)

**Répertoire :** `/frontend/src/components/ui/`

**Composants disponibles :**
- **Button** (`button.tsx`) - Boutons stylisés avec variants
- **Badge** (`badge.tsx`) - Badges pour statuts et catégories
- **Table** (`table.tsx`) - Tableaux pour données tabulaires
- **Dialog** (`dialog.tsx`) - Modales et dialogues
- **Card** (`card.tsx`) - Cartes pour conteneurs
- **Input** (`input.tsx`) - Champs de formulaire
- **Select** (`select.tsx`) - Menus déroulants
- **Tabs** (`tabs.tsx`) - Navigation par onglets

**Exemple d'utilisation - Button :**
```typescript
import { Button } from '../components/ui/button';

<Button variant="default">Ajouter au panier</Button>
<Button variant="destructive">Supprimer</Button>
<Button variant="outline">Annuler</Button>
<Button variant="ghost">Fermer</Button>
```

**Exemple d'utilisation - Badge :**
```typescript
import { Badge } from '../components/ui/badge';

<Badge variant="default">En stock</Badge>
<Badge variant="destructive">Épuisé</Badge>
<Badge variant="secondary">-20%</Badge>
```

### 📹 À montrer dans la vidéo :
- [ ] Montrer différents boutons avec variants
- [ ] Montrer les badges de statut
- [ ] Montrer un tableau avec les composants Table
- [ ] Mentionner : "Design system cohérent avec Shadcn/ui"

**Durée : 20 secondes**

---

### 4. Gestion d'images (Base64)

**Code clé :**
```typescript
// Upload et conversion en Base64
const handleImageChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  const file = e.target.files?.[0];
  if (file) {
    // Validation du type
    if (!file.type.startsWith('image/')) {
      alert('Veuillez sélectionner une image');
      return;
    }
    
    // Conversion en Base64
    const reader = new FileReader();
    reader.onloadend = () => {
      const base64String = reader.result as string;
      setFormData({ ...formData, image: base64String });
    };
    reader.readAsDataURL(file);
  }
};

// Affichage
<img src={product.image} alt={product.name} />
```

**Avantages :**
- Pas de serveur de fichiers nécessaire
- Stockage direct en base de données
- Simplicité de déploiement

### 📹 À montrer dans la vidéo :
- [ ] Lors de l'ajout de produit, montrer l'upload d'image
- [ ] Montrer le preview de l'image
- [ ] Expliquer : "Images stockées en Base64 pour simplicité"

**Durée : 15 secondes**

---

### 5. Responsive Design et accessibilité

**Utilisation de Tailwind CSS :**
```typescript
// Classes responsive
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
  {/* Mobile: 1 colonne, Tablet: 2, Desktop: 3, Large: 4 */}
</div>

// Classes conditionnelles
<button className="hidden md:block">Visible uniquement desktop</button>
<button className="block md:hidden">Visible uniquement mobile</button>
```

**Composants accessibles :**
- Labels pour tous les inputs
- ARIA labels pour les icônes
- Contraste de couleurs conforme WCAG
- Navigation au clavier

### 📹 À montrer dans la vidéo :
- [ ] Redimensionner la fenêtre du navigateur
- [ ] Montrer la grille s'adapter (4→3→2→1 colonnes)
- [ ] Montrer le menu mobile vs desktop
- [ ] Mentionner : "100% responsive et accessible"

**Durée : 20 secondes**

---

## 🎬 Guide Vidéo Parallèle - Structure Complète

### 📝 Plan de tournage recommandé

**Durée totale : 10-12 minutes**

---

### **Partie 1 : Introduction (1 minute)**
- [ ] **0:00-0:15** - Écran de titre "El Bazar - E-commerce Platform"
- [ ] **0:15-0:30** - Vue d'ensemble : Backend terminal + Frontend navigateur
- [ ] **0:30-0:45** - Montrer la structure du projet dans l'éditeur
- [ ] **0:45-1:00** - Transition vers les fonctionnalités

**Script :** "Bienvenue dans El Bazar, une plateforme e-commerce complète avec React, TypeScript, Node.js et Prisma."

---

### **Partie 2 : Authentification (2 minutes)**
- [ ] **1:00-1:30** - Inscription vendeur avec tous les champs
- [ ] **1:30-1:45** - Redirection automatique vers dashboard
- [ ] **1:45-2:15** - Déconnexion + Connexion acheteur
- [ ] **2:15-3:00** - Montrer la différence de navigation selon le rôle

**Script :** "Le système d'authentification distingue automatiquement acheteurs et vendeurs, avec des interfaces dédiées."

---

### **Partie 3 : Expérience Acheteur (3 minutes)**
- [ ] **3:00-3:30** - Page d'accueil : liste des vendeurs
- [ ] **3:30-4:30** - Page produits : filtres, tri, vue grille/liste
- [ ] **4:30-5:15** - Gestion du panier : ajout, modification, total
- [ ] **5:15-5:45** - Passage de commande
- [ ] **5:45-6:00** - Mes commandes : suivi

**Script :** "Les acheteurs bénéficient d'une expérience complète : navigation intuitive, filtres avancés, panier persistant."

---

### **Partie 4 : Tableau de Bord Vendeur (4 minutes)**
- [ ] **6:00-6:30** - Statistiques du dashboard
- [ ] **6:30-7:30** - CRUD produits : création avec image
- [ ] **7:30-8:00** - Modification et suppression
- [ ] **8:00-8:45** - Gestion des commandes + changement de statut
- [ ] **8:45-9:15** - Profil de boutique (vue publique)

**Script :** "Les vendeurs ont un contrôle total : gestion des produits, suivi des commandes, statistiques en temps réel."

---

### **Partie 5 : Fonctionnalités Avancées (2 minutes)**
- [ ] **9:15-10:00** - Chatbot avec conversation
- [ ] **10:00-10:20** - Code : Montrer les hooks React
- [ ] **10:20-10:40** - Responsive design (redimensionnement)
- [ ] **10:40-11:00** - Composants UI Shadcn

**Script :** "Technologies modernes : hooks React pour la performance, chatbot IA, design responsive."

---

### **Partie 6 : Architecture Technique (1 minute)**
- [ ] **11:00-11:20** - Ouvrir schema.prisma (modèles de données)
- [ ] **11:20-11:40** - Montrer un contrôleur backend
- [ ] **11:40-12:00** - Montrer un service frontend

**Script :** "Architecture propre avec séparation des responsabilités : Prisma ORM, contrôleurs Express, services React."

---

### **Conclusion (30 secondes)**
- [ ] **12:00-12:15** - Récapitulatif rapide des fonctionnalités
- [ ] **12:15-12:30** - Écran final avec logo et remerciements

**Script :** "El Bazar : une solution e-commerce complète, moderne et prête pour la production. Merci !"

---

## 🎥 Conseils de Tournage

### Préparation
1. **Préparer les données de démonstration :**
   - 3-4 vendeurs avec logos
   - 10-15 produits variés avec images
   - Quelques commandes de test

2. **Configuration de l'écran :**
   - Résolution : 1920x1080
   - Zoom navigateur : 100%
   - Police de code lisible (14-16pt)

3. **Outils recommandés :**
   - OBS Studio pour l'enregistrement
   - Screencast-O-Matic
   - Loom

### Pendant le tournage
- **Rythme :** Ni trop rapide, ni trop lent
- **Curseur :** Bien visible, mouvements fluides
- **Pauses :** Laisser 2-3 secondes après chaque action importante
- **Transitions :** Fluides entre les sections
- **Zoom :** Utiliser le zoom pour montrer les détails de code

### Éléments à mettre en avant
- ✅ Animations et transitions fluides
- ✅ Réactivité de l'interface
- ✅ Cohérence du design
- ✅ Fonctionnalités complètes (du début à la fin)
- ✅ Code propre et organisé

---

## 📊 Tableau récapitulatif : Fonctionnalités → Code → Vidéo

| Fonctionnalité | Fichier Principal | Code Clé (Lignes) | Durée Vidéo | Ordre |
|----------------|-------------------|-------------------|-------------|-------|
| Architecture App | `/frontend/App.tsx` | 1-260 | 30s | 1 |
| Inscription | `/frontend/src/components/RegisterForm.tsx` | 80-150 | 45s | 2 |
| Connexion | `/frontend/src/components/Login.tsx` | 40-80 | 30s | 3 |
| Page d'accueil | `/frontend/src/pages/HomePage.tsx` | 45-70 | 30s | 4 |
| Page Produits | `/frontend/src/pages/ProductsPage.tsx` | 39-120 | 1m | 5 |
| Panier | `/frontend/App.tsx` | 135-164 | 1m15s | 6 |
| Commande | `/frontend/src/services/orderService.ts` | Toutes | 45s | 7 |
| Mes Commandes | `/frontend/src/pages/MyOrdersPage.tsx` | Toutes | 30s | 8 |
| Dashboard Vendeur | `/frontend/src/pages/SellerDashboard.tsx` | 34-120 | 30s | 9 |
| CRUD Produits | `/frontend/src/components/ProductForm.tsx` | Toutes | 2m15s | 10 |
| Commandes Vendeur | `/frontend/src/pages/SellerDashboard.tsx` | 300-400 | 45s | 11 |
| Profil Boutique | `/frontend/src/pages/StoreProfilePage.tsx` | Toutes | 30s | 12 |
| Chatbot | `/frontend/src/pages/ChatBotPage.tsx` | Toutes | 45s | 13 |
| Hooks React | `/frontend/App.tsx` | 65-180 | 30s | 14 |
| Composants UI | `/frontend/src/components/ui/*` | Tous | 20s | 15 |

---

## 🔑 Points Clés à Mentionner

### Technologies
- ✅ **React 18** avec TypeScript
- ✅ **Vite** pour le build ultra-rapide
- ✅ **Tailwind CSS** pour le styling
- ✅ **Shadcn/ui** pour les composants
- ✅ **Prisma ORM** pour la base de données
- ✅ **JWT** pour l'authentification
- ✅ **SQLite** (dev) / PostgreSQL (prod ready)

### Fonctionnalités Métier
- ✅ Double rôle utilisateur (Acheteur/Vendeur)
- ✅ Gestion complète du catalogue
- ✅ Panier persistant
- ✅ Système de commandes complet
- ✅ Dashboard vendeur avec statistiques
- ✅ Chatbot IA

### Bonnes Pratiques
- ✅ Séparation frontend/backend
- ✅ Architecture composants réutilisables
- ✅ Hooks React pour optimisation
- ✅ TypeScript pour la sécurité des types
- ✅ Responsive design
- ✅ Accessibilité WCAG

---

## 📝 Notes Finales

### Personnalisation du script
Vous pouvez adapter ce script selon :
- Le public cible (technique vs business)
- La durée souhaitée (version courte 5min vs complète 12min)
- Les fonctionnalités prioritaires

### Synchronisation Code-Vidéo
Pour chaque fonctionnalité montrée :
1. **Montrer l'interface** (résultat)
2. **Montrer le code** (implémentation)
3. **Expliquer la logique** (comment ça marche)

### Ressources additionnelles
- **README.md** : Documentation utilisateur
- **USER_GUIDE.md** : Guide d'utilisation détaillé
- **IMPLEMENTATION_SUMMARY.md** : Résumé technique
- **DATABASE_FIX_SUMMARY.md** : Architecture base de données

---

**Créé pour le projet El Bazar**  
**Licence : MIT**  
**Version : 1.0**
