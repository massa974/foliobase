# Portfolio Template - Graphiste Freelance

Un template moderne et professionnel pour créer un portfolio de graphiste freelance utilisant Next.js, Tailwind CSS et Decap CMS.

## 🚀 Fonctionnalités

- ✅ **Next.js 15** avec App Router
- ✅ **Tailwind CSS 3.x** pour le styling
- ✅ **shadcn/ui** pour les composants
- ✅ **Decap CMS** pour la gestion de contenu
- ✅ **Cloudinary** pour les images
- ✅ **TypeScript** pour la robustesse
- ✅ **Responsive design** mobile-first
- ✅ **Export statique** pour Netlify
- ✅ **SEO optimisé**

## 📋 Prérequis

- Node.js 18+ 
- pnpm (recommandé) ou npm
- Un compte GitHub
- Un compte Netlify
- Un compte Cloudinary (gratuit)

## 🛠️ Installation

### 1. Cloner le repository

```bash
git clone <votre-repo>
cd portfolio-template
```

### 2. Installer les dépendances

```bash
pnpm install
```

### 3. Configurer Cloudinary

1. Créez un compte sur [Cloudinary](https://cloudinary.com/)
2. Récupérez votre `cloud_name` et `api_key` dans le dashboard
3. Modifiez `public/admin/config.yml` :

```yaml
media_library:
  name: cloudinary
  config:
    cloud_name: VOTRE_CLOUD_NAME
    api_key: VOTRE_API_KEY
```

### 4. Lancer le serveur de développement

```bash
# Terminal 1 : Serveur Decap CMS (pour le développement local)
npx decap-server

# Terminal 2 : Application Next.js
pnpm dev
```

Ouvrez [http://localhost:3000](http://localhost:3000) pour voir votre portfolio.
Accédez à [http://localhost:3000/admin](http://localhost:3000/admin) pour le CMS.

## 🌐 Déploiement sur Netlify

### 1. Pousser sur GitHub

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### 2. Connecter à Netlify

1. Allez sur [Netlify](https://netlify.com)
2. Cliquez sur "New site from Git"
3. Connectez votre repository GitHub
4. Configuration :
   - **Build command**: `pnpm build`
   - **Publish directory**: `out`

### 3. Configurer l'authentification

#### Netlify Identity

1. Dans votre dashboard Netlify : `Site settings > Identity`
2. Cliquez sur "Enable Identity"
3. Configurez les options :
   - **Registration**: "Invite only" (recommandé)
   - **External providers**: GitHub (optionnel)

#### Git Gateway

1. Toujours dans Identity : `Services > Git Gateway`
2. Cliquez sur "Enable Git Gateway"

### 4. Créer un utilisateur admin

1. Dans Identity, cliquez sur "Invite users"
2. Invitez-vous avec votre email
3. Vérifiez votre email et définissez un mot de passe

## ✏️ Utilisation du CMS

### Accéder au CMS

- **En local**: `http://localhost:3000/admin`
- **En production**: `https://votre-site.netlify.app/admin`

### Gérer le contenu

#### Pages statiques

- **Accueil**: Titre, sous-titre, description, bouton CTA
- **À propos**: Bio, compétences, photo de profil

#### Projets

- **Informations générales**: Titre, client, type, statut
- **Médias**: Image principale, galerie d'images
- **Fichiers**: PDF portfolio (< 20MB recommandé)
- **Description**: Contenu Markdown riche

### Structure des fichiers

```
content/
├── pages/
│   ├── homepage.md
│   └── about.md
└── projects/
    ├── 2024-01-15-mon-premier-projet.md
    └── 2024-02-20-identite-visuelle-startup.md
```

## 🎨 Personnalisation

### Couleurs et thème

Modifiez `tailwind.config.js` pour personnaliser les couleurs :

```js
theme: {
  extend: {
    colors: {
      primary: {
        // Vos couleurs personnalisées
      },
    },
  },
},
```

### Logo et favicon

- Remplacez le logo dans `src/components/layout/header.tsx`
- Ajoutez votre favicon dans `public/`

### Métadonnées

Modifiez `src/app/layout.tsx` pour vos informations :

```tsx
export const metadata: Metadata = {
  title: "Votre Nom - Graphiste Freelance",
  description: "Votre description personnalisée",
  // ...
}
```

## 📁 Structure du projet

```
src/
├── app/                    # Pages Next.js
│   ├── about/             # Page à propos
│   ├── projects/          # Pages projets
│   └── layout.tsx         # Layout principal
├── components/
│   ├── layout/            # Header, Footer
│   └── ui/                # Composants shadcn/ui
└── lib/
    ├── content.ts         # Utilitaires contenu
    └── utils.ts           # Utilitaires shadcn

content/                   # Contenu Markdown
├── pages/                 # Pages statiques
└── projects/              # Projets

public/
├── admin/                 # Configuration Decap CMS
│   ├── index.html
│   └── config.yml
└── uploads/               # Fallback pour gros fichiers
```

## 🔧 Scripts disponibles

```bash
# Développement
pnpm dev                   # Serveur de développement

# Build et déploiement
pnpm build                 # Build de production
pnpm start                 # Serveur de production

# CMS local
npx decap-server          # Serveur CMS pour développement

# Linting
pnpm lint                 # Vérification du code
```

## 📝 Bonnes pratiques

### Images

- **Formats supportés**: JPG, PNG, WebP, GIF
- **Taille recommandée**: 
  - Images principales : 1200x800px
  - Galeries : 800x600px
  - Photos de profil : 400x400px

### PDF

- **Taille maximale recommandée**: 20MB
- **Formats acceptés**: PDF uniquement
- **Utilisation**: CV, portfolios, présentations

### Contenu

- **Titres**: Courts et percutants
- **Descriptions**: 150-200 caractères pour les extraits
- **Mots-clés**: Utilisez des termes pertinents pour le SEO

## 🆘 Dépannage

### Problèmes courants

#### Le CMS ne charge pas
- Vérifiez que `npx decap-server` fonctionne en local
- Vérifiez la configuration Git Gateway sur Netlify

#### Images qui ne s'affichent pas
- Vérifiez votre configuration Cloudinary
- Assurez-vous que les clés API sont correctes

#### Erreurs de build
- Vérifiez que tous les fichiers Markdown ont un front-matter valide
- Vérifiez la syntaxe YAML dans `config.yml`

## 📚 Ressources

- [Documentation Next.js](https://nextjs.org/docs)
- [Documentation Decap CMS](https://decapcms.org/docs/)
- [Documentation Tailwind CSS](https://tailwindcss.com/docs)
- [Composants shadcn/ui](https://ui.shadcn.com/)
- [Documentation Cloudinary](https://cloudinary.com/documentation)
- [Guide Netlify](https://docs.netlify.com/)

## 📄 Licence

Ce template est sous licence MIT. Vous êtes libre de l'utiliser pour vos projets personnels et commerciaux.

---

**Créé avec ❤️ pour les étudiants en design graphique**
