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
- ✅ **Authentification GitHub** (simple et gratuite)

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

### 4. Configurer le repository GitHub

1. Modifiez `public/admin/config.yml` avec votre repository :

```yaml
backend:
  name: github
  repo: votre-username/nom-du-repository
  branch: main
```

### 5. Lancer le serveur de développement

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

### 3. Configurer l'authentification GitHub

#### ⚠️ **Important :** Netlify Identity est déprécié depuis février 2025. Ce template utilise maintenant l'authentification GitHub directe.

#### Configuration automatique

L'authentification GitHub fonctionne automatiquement avec Decap CMS ! Aucune configuration supplémentaire n'est nécessaire sur Netlify.

**Comment ça marche :**
1. Les utilisateurs vont sur `https://votre-site.netlify.app/admin`
2. Ils cliquent sur "Login with GitHub"
3. GitHub demande l'autorisation d'accès au repository
4. Une fois autorisé, l'utilisateur peut modifier le contenu

#### Permissions requises

Les utilisateurs doivent avoir **accès en écriture** au repository GitHub pour pouvoir modifier le contenu :
- **Propriétaire** : Accès complet automatique
- **Collaborateurs** : Ajouter via GitHub Settings > Manage access > Invite a collaborator
- **Membres d'organisation** : Configurer les permissions au niveau de l'organisation

## ✏️ Utilisation du CMS

### Accéder au CMS

- **En local**: `http://localhost:3000/admin`
- **En production**: `https://votre-site.netlify.app/admin`

### Première connexion

1. Allez sur `/admin` de votre site déployé
2. Cliquez sur **"Login with GitHub"**
3. Autorisez l'application à accéder à votre repository
4. ✅ Vous pouvez maintenant créer et modifier du contenu !

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

## 👥 Gestion des utilisateurs

### Ajouter des utilisateurs (pour les enseignants)

Pour permettre à vos étudiants d'accéder au CMS :

1. **Repository privé** : Ajoutez-les comme collaborateurs
   - GitHub Repository > Settings > Manage access
   - Invite a collaborator
   - Rôle : **Write** (pour modifier le contenu)

2. **Repository public** : Les étudiants peuvent fork
   - Ils créent leur propre repository
   - Modifient la config avec leur repository
   - Déploient leur propre version

### Permissions par défaut

- ✅ **Propriétaire** : Accès complet
- ✅ **Collaborateurs Write** : Peut créer/modifier le contenu
- ❌ **Collaborateurs Read** : Lecture seule (pas d'accès CMS)

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
- Vérifiez la configuration du repository dans `config.yml`
- Assurez-vous d'avoir les permissions d'écriture sur le repository

#### "Error loading the CMS configuration"
- Vérifiez la syntaxe YAML dans `public/admin/config.yml`
- Assurez-vous que le repository GitHub existe et est accessible

#### Images qui ne s'affichent pas
- Vérifiez votre configuration Cloudinary
- Assurez-vous que les clés API sont correctes

#### Erreurs de build
- Vérifiez que tous les fichiers Markdown ont un front-matter valide
- Vérifiez la syntaxe YAML dans `config.yml`

#### "Failed to persist entry"
- L'utilisateur n'a pas les permissions d'écriture sur le repository
- Ajoutez l'utilisateur comme collaborateur avec le rôle "Write"

## 🎓 Guide pour les étudiants

### Configuration rapide

1. **Forkez** ce repository
2. **Modifiez** `public/admin/config.yml` avec votre repository :
   ```yaml
   backend:
     name: github
     repo: votre-username/portfolio-template
     branch: main
   ```
3. **Configurez** Cloudinary avec vos clés
4. **Déployez** sur Netlify
5. **Accédez** à `/admin` et connectez-vous avec GitHub

### Workflow recommandé

1. 📝 **Développement local** avec `pnpm dev`
2. ✨ **Ajout de contenu** via `/admin`
3. 🚀 **Push automatique** vers GitHub
4. 🌐 **Déploiement automatique** sur Netlify

## 🔄 Migration depuis Netlify Identity

Si vous avez un projet existant avec Netlify Identity :

### Étapes de migration

1. **Sauvegardez** vos utilisateurs Netlify Identity
2. **Modifiez** `public/admin/config.yml` :
   ```yaml
   # Remplacez :
   backend:
     name: git-gateway
     branch: main
   
   # Par :
   backend:
     name: github
     repo: username/repository-name
     branch: main
   ```
3. **Supprimez** les redirects liés à Identity dans `netlify.toml`
4. **Redéployez** votre site
5. **Informez** les utilisateurs de se connecter avec GitHub

### Avantages de la migration

- ✅ **Plus simple** à configurer et maintenir
- ✅ **Gratuit** et illimité
- ✅ **Pas de dépendance** aux services dépréciés
- ✅ **Meilleure** formation technique pour les étudiants

## 📚 Ressources

- [Documentation Next.js](https://nextjs.org/docs)
- [Documentation Decap CMS](https://decapcms.org/docs/)
- [Documentation Tailwind CSS](https://tailwindcss.com/docs)
- [Composants shadcn/ui](https://ui.shadcn.com/)
- [Documentation Cloudinary](https://cloudinary.com/documentation)
- [Guide Netlify](https://docs.netlify.com/)
- [Guide GitHub Collaborators](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository)

## 📄 Licence

Ce template est sous licence MIT. Vous êtes libre de l'utiliser pour vos projets personnels et commerciaux.

---

**✨ Mise à jour 2025 : Authentification GitHub directe**
**Plus besoin de Netlify Identity ! Configuration simplifiée et 100% gratuite.**

**Créé avec ❤️ pour les étudiants en design graphique**
