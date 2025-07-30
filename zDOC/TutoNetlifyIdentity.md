# 🔐 Tutoriel : Activation de Netlify Identity et Git Gateway

## ⚠️ **AVERTISSEMENT IMPORTANT - Dépréciation**

**Netlify Identity et Git Gateway sont officiellement dépréciés depuis février 2025.**

- ✅ **Continuent de fonctionner** pour les sites existants
- ❌ **Pas de nouvelles fonctionnalités** ni corrections de bugs
- ⚡ **Uniquement les correctifs de sécurité majeurs**

### 🔄 **Alternatives recommandées :**
- **Pour Netlify Identity** → [Auth0 Extension](https://docs.netlify.com/integrations/auth0/)
- **Pour GoTrue API** → [Supabase Auth](https://supabase.com/auth)

> **Note :** Ce tutoriel reste valide pour des projets éducatifs ou des sites existants, mais pour de nouveaux projets en production, considérez les alternatives ci-dessus.

---

## 📋 **Prérequis**

Avant de commencer, assurez-vous d'avoir :

- ✅ Un compte Netlify
- ✅ Un site déployé sur Netlify
- ✅ Un repository GitHub connecté à Netlify
- ✅ Un domaine HTTPS (obligatoire pour Identity)

---

## 🚀 **Étape 1 : Activer Netlify Identity**

### 1.1 Accéder au Dashboard Netlify

1. Connectez-vous à [netlify.com](https://netlify.com)
2. Sélectionnez votre site dans la liste
3. Allez dans **Site settings** (Paramètres du site)

### 1.2 Activer Identity

1. Dans le menu latéral, cliquez sur **Identity**
2. Cliquez sur **Enable Identity** (Activer Identity)

![Netlify Identity Activation](https://docs.netlify.com/images/identity-enable.png)

### 1.3 Configuration des paramètres Identity

Une fois activé, vous verrez l'URL de l'API Identity :
```
https://votre-site.netlify.app/.netlify/identity
```

**Copiez cette URL**, vous en aurez besoin plus tard !

---

## ⚙️ **Étape 2 : Configurer les paramètres d'inscription**

### 2.1 Paramètres d'inscription

1. Dans **Identity**, cliquez sur **Settings and usage**
2. Dans **Registration preferences** :
   - **Invite only** : Seuls les utilisateurs invités peuvent s'inscrire (recommandé)
   - **Open** : N'importe qui peut s'inscrire

### 2.2 Configuration des emails de confirmation

1. Allez dans **Emails** → **Confirmation template**
2. Cliquez sur **Edit settings**
3. **Option recommandée pour les portfolios** :
   - ✅ Cochez "Allow users to sign up without verifying their email address"
   - Cliquez **Save**

### 2.3 Fournisseurs d'authentification externes (optionnel)

Dans **External providers**, vous pouvez activer :
- 🔵 **Google** (gratuit)
- ⚫ **GitHub** (gratuit)
- 🟠 **GitLab** (gratuit)
- 💼 **OAuth providers** (payants)

---

## 🔗 **Étape 3 : Activer Git Gateway**

### 3.1 Prérequis pour Git Gateway

- ✅ Netlify Identity doit être activé
- ✅ Repository sur GitHub.com ou GitLab.com (pas les versions self-hosted)
- ✅ Domaine HTTPS configuré

### 3.2 Activation

1. Dans **Identity**, allez dans **Services**
2. Cherchez **Git Gateway**
3. Cliquez sur **Enable Git Gateway**

### 3.3 Configuration automatique

Netlify va automatiquement :
- Créer une connexion avec votre repository
- Configurer les permissions nécessaires
- Générer un token d'accès

---

## 🎯 **Étape 4 : Configuration des rôles (optionnel)**

### 4.1 Création de rôles

1. Dans **Identity** → **Settings and usage**
2. Dans **Roles**, ajoutez des rôles comme :
   - `admin` : Accès complet
   - `editor` : Modification de contenu
   - `viewer` : Lecture seule

### 4.2 Configuration Git Gateway avec rôles

1. Retournez dans **Services** → **Git Gateway**
2. Dans **Roles**, spécifiez quels rôles ont accès :
   - Laissez vide = tous les utilisateurs Identity
   - Spécifiez `admin` = seuls les admins

---

## 👥 **Étape 5 : Créer le premier utilisateur admin**

### 5.1 Inviter un utilisateur

1. Dans **Identity**, cliquez sur **Invite users**
2. Entrez votre email
3. Cliquez **Send**

### 5.2 Accepter l'invitation

1. Vérifiez votre email
2. Cliquez sur le lien d'invitation
3. Créez votre mot de passe
4. Confirmez votre compte

### 5.3 Assigner un rôle admin

1. Dans le dashboard Netlify → **Identity** → **Users**
2. Cliquez sur votre utilisateur
3. Dans **Roles**, ajoutez `admin`
4. Sauvegardez

---

## 🧪 **Étape 6 : Tester la configuration**

### 6.1 Accéder au CMS

1. Allez sur `https://votre-site.netlify.app/admin`
2. Connectez-vous avec vos identifiants Identity
3. Vous devriez voir l'interface Decap CMS

### 6.2 Vérifications

- ✅ **Login/Logout** fonctionne
- ✅ **Interface CMS** s'affiche
- ✅ **Collections** sont visibles
- ✅ **Médias Cloudinary** fonctionnent

---

## 🔧 **Étape 7 : Configuration avancée**

### 7.1 Tokens d'accès personnalisés

Si vous avez des problèmes avec GitLab ou des permissions spécifiques :

1. **GitHub** : Générez un Personal Access Token avec les scopes :
   - `repo` (accès au repository)
   - `workflow` (pour les actions GitHub)

2. **GitLab** : Créez un Personal Access Token avec :
   - `api`
   - `read_api`
   - `read_repository` 
   - `write_repository`

### 7.2 Ajouter le token personnalisé

1. Dans **Git Gateway** → **Settings**
2. Collez votre token dans **Access token**
3. Sauvegardez

---

## 🚨 **Dépannage courant**

### Problème : "Git Gateway ne se connecte pas"

**Solutions :**
1. Vérifiez que HTTPS est activé
2. Reconnectez le repository :
   - **Build & deploy** → **Repository** → **Manage repository**
   - Cliquez **Link to a different repository**
   - Resélectionnez le même repository

### Problème : "L'interface CMS ne charge pas"

**Solutions :**
1. Vérifiez l'URL dans `public/admin/config.yml`
2. Contrôlez les erreurs dans la console navigateur
3. Assurez-vous que `netlify.toml` a les redirects corrects

### Problème : "Erreur de permissions GitLab"

**Solution :**
- GitLab 15.0+ nécessite des tokens avec expiration
- Générez un nouveau Personal Access Token
- Ajoutez-le dans Git Gateway settings

---

## 📊 **Limites du plan gratuit**

### Netlify Identity (gratuit)
- ✅ **1,000 utilisateurs actifs** par mois
- ✅ **5 invitations** par mois
- ❌ Pas de fournisseurs OAuth premium

### Git Gateway (gratuit)
- ✅ **Accès API illimité** au repository
- ✅ **Pas de limite de commits**
- ❌ Seulement GitHub.com et GitLab.com

---

## 🔒 **Bonnes pratiques de sécurité**

### Pour les étudiants

1. **Utilisez des mots de passe forts**
2. **Activez la vérification email** en production
3. **Limitez aux rôles nécessaires**
4. **Surveillez les connexions** dans Identity audit log

### Pour l'enseignant

1. **Mode "Invite only"** recommandé
2. **Créez des rôles spécifiques** par promotion
3. **Surveillez l'usage** dans Identity dashboard
4. **Sauvegardez la liste des utilisateurs** régulièrement

---

## 📝 **Configuration Cloudinary dans le projet**

Une fois Netlify Identity et Git Gateway activés, n'oubliez pas de configurer Cloudinary dans votre `public/admin/config.yml` :

```yaml
media_library:
  name: cloudinary
  config:
    cloud_name: votre_cloud_name
    api_key: votre_api_key
    multiple: true
```

---

## 🎓 **Instructions pour les étudiants**

### Étapes rapides pour un nouvel étudiant :

1. **Recevoir l'invitation** par email
2. **Cliquer sur le lien** d'activation
3. **Créer un mot de passe** sécurisé
4. **Se connecter** sur `https://votre-portfolio.netlify.app/admin`
5. **Commencer à créer du contenu** !

---

## 🆘 **Support et ressources**

### En cas de problème :

1. **Documentation officielle** : [docs.netlify.com](https://docs.netlify.com)
2. **Community forum** : [answers.netlify.com](https://answers.netlify.com)
3. **Support Netlify** (pour migration) : [netlify.com/support](https://netlify.com/support)

### Alternatives futures :

- **Auth0** : [Extension officielle Netlify](https://docs.netlify.com/integrations/auth0/)
- **Supabase Auth** : [Fork maintenu de GoTrue](https://supabase.com/auth)
- **Firebase Auth** : [Google authentication](https://firebase.google.com/docs/auth)

---

## ✅ **Checklist finale**

Avant de considérer la configuration terminée :

- [ ] Netlify Identity activé
- [ ] Git Gateway activé
- [ ] Premier utilisateur admin créé
- [ ] Rôles configurés (si nécessaire)
- [ ] Test de connexion CMS réussi
- [ ] Cloudinary configuré
- [ ] Repository connecté
- [ ] HTTPS fonctionnel
- [ ] Redirects Netlify en place

---

**🎉 Félicitations ! Votre template de portfolio est maintenant prêt à être utilisé par vos étudiants !**
