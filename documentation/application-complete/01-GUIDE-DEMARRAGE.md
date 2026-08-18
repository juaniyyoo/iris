# Guide de Démarrage - Projet NathAnimÂge

## 🎯 Vue d'ensemble du projet

Vous créez une application web pour documenter les animations auprès de seniors en quelques minutes. L'app combine trois éléments clés :
- **🎙️ Enregistrements audio** : Capturer des moments de vie
- **📸 Photos** : Documenter les activités
- **🤖 IA générative** : Transformer notes et enregistrements en comptes rendus professionnels

L'application se divise en deux espaces :
- **Animatrice** : Outil de documentation (web)
- **Famille** : Journal de vie privé (web + mobile)

---

## 🏗️ Architecture générale

```
NathAnimÂge (Votre Projet)
├── Frontend (React + TypeScript)
│   ├── Web - Interface animatrice (Expo Web)
│   ├── Mobile - Journal famille (React Native via Expo)
│   └── Gestion d'état (Redux Toolkit)
│
├── Backend (Python)
│   ├── API REST (FastAPI)
│   ├── Traitement audio (Whisper API)
│   ├── Génération texte (Claude/OpenAI)
│   ├── Stockage fichiers (S3)
│   └── Base de données (PostgreSQL)
│
└── Services externes
    ├── OpenAI/Anthropic (IA générative)
    ├── AWS S3 (Stockage photos/audio)
    └── Firebase Auth (Authentification)
```

**Pourquoi cette architecture ?**
- **Frontend unique** : Un seul codebase (React + React Native) pour web et mobile
- **Backend simplifié en Python** : Plus facile à maintenir et déployer
- **Séparation claire** : Le frontend ne parle qu'à l'API, jamais directement aux services externes

---

## 📚 Les briques technologiques (expliquées simplement)

### Frontend - Ce que voient les utilisateurs

**React** : Bibliothèque pour construire des interfaces. Pense à LEGO - tu construis des petits blocs (composants) que tu combines.

**React Native** : Permet d'utiliser React pour faire des apps mobile iOS et Android. Sans React Native, tu devrais écrire du code différent pour iPhone et Android.

**Expo** : Fait que tu peux tester ton app mobile sur ton téléphone sans compiler. C'est comme un raccourci de développement.

**Redux Toolkit** : Système de rangement centralisé pour tes données. Plutôt que de passer les infos de composant en composant, tout est au même endroit.

**TypeScript** : C'est JavaScript + des règles. Ça t'aide à repérer les erreurs avant même de lancer le code.

### Backend - Ce qui fait fonctionner l'app côté serveur

**FastAPI** : Framework Python ultra-rapide pour créer des APIs (l'intermédiaire entre ton frontend et la base de données).

**PostgreSQL** : Base de données. C'est comme un tableau Excel géant et ultra-puissant où tu stockes toutes tes infos.

**Python** : Langage de programmation super lisible. Beaucoup plus facile qu'autres langages pour quelqu'un qui débute.

**Whisper API** (OpenAI) : Transforme l'audio en texte automatiquement.

**Claude/GPT-4** (IA) : Transforme les notes brutes en comptes rendus professionnels et bien écrits.

**AWS S3** : Service de stockage dans le cloud. C'est où tu ranges les photos et les enregistrements audio.

---

## 🚀 Flux de l'utilisateur (ce qui se passe)

### 1️⃣ Animatrice documente une séance

```
Animatrice ouvre l'app
    ↓
Choisit le senior + crée une nouvelle séance
    ↓
Pendant la séance :
  - Prend des photos
  - Enregistre des audio
  - Écrit des notes
    ↓
Termine la séance
    ↓
Clique "Générer le compte rendu"
```

### 2️⃣ Le backend se met au travail

```
Données envoyées au backend
    ↓
L'audio est transcrit en texte (Whisper)
    ↓
Tout (photos, texte, notes) est envoyé à Claude/GPT
    ↓
Claude génère un joli compte rendu
    ↓
Les photos sont compressées et envoyées à S3
    ↓
Les données sont sauvegardées en base de données
```

### 3️⃣ Famille reçoit le compte rendu

```
La famille peut voir :
  - La date et heure
  - Un texte bien rédigé
  - Les photos
  - Les audio (instants marquants)
```

---

## 📊 Modèle économique

- **Gratuit** : Jusqu'à 5 seniors
- **Payant** : Au-delà, 15€/mois

La limite est vérifiée côté backend (backend.py) pour empêcher les contournements.

---

## 🎬 Comment démarrer - Étapes recommandées

### Phase 1 : Mise en place (1-2 jours)
1. ✅ Créer la structure du projet (voir prompt)
2. ✅ Configurer les outils (Node.js, Python)
3. ✅ Configurer les variables d'environnement

### Phase 2 : Backend de base (3-5 jours)
1. ✅ Créer les endpoints API principaux
2. ✅ Intégrer Whisper (transcription audio)
3. ✅ Intégrer Claude/GPT-4 (génération texte)
4. ✅ Configurer PostgreSQL
5. ✅ Tester les endpoints avec Postman

### Phase 3 : Frontend base (5-7 jours)
1. ✅ Créer l'authentification (login/signup)
2. ✅ Page pour créer une séance
3. ✅ Page pour enregistrer et prendre des photos
4. ✅ Page pour voir les comptes rendus générés

### Phase 4 : Stockage fichiers (2-3 jours)
1. ✅ Configurer AWS S3
2. ✅ Uploader photos/audio vers S3
3. ✅ Afficher les fichiers depuis S3

### Phase 5 : Polish et déploiement (en continu)
1. ✅ Tests
2. ✅ Corrections de bugs
3. ✅ Optimisations
4. ✅ Déploiement en production

---

## 🔐 Points importants à retenir

### Sécurité
- ⚠️ Les données sont sensibles (personnes âgées)
- ⚠️ Toujours authentifier les requêtes
- ⚠️ Chiffrer les données en transit (HTTPS)

### RGPD
- 🇪🇺 Loi française s'applique
- ⚠️ Droit à l'oubli (pouvoir supprimer ses données)
- ⚠️ Consentement explicite pour audio/photos

### Performance
- 📸 Compresser les photos avant upload
- 🎙️ L'audio peut être lourd - limiter la qualité si nécessaire
- ⏱️ Les appels IA (Claude/Whisper) peuvent être lents

---

## 📖 Ressources pratiques

- **Déploiement frontend** : Vercel (gratuit, ultra simple)
- **Déploiement backend** : Railway ou Render (gratuit tier disponible)
- **Base de données** : Railway ou neon.tech (PostgreSQL gratuit)
- **Stockage fichiers** : AWS S3 (gratuit jusqu'à 5GB)

---

## 🆘 Besoin d'aide ?

Chaque technologie a sa documentation officielle :
- React : https://react.dev
- React Native + Expo : https://docs.expo.dev
- FastAPI : https://fastapi.tiangolo.com
- PostgreSQL : https://www.postgresql.org/docs

Commencez par lire les "Getting Started" sur chaque site.

---

## Prochaine étape

👉 **Lisez le prompt pour générer la structure du projet** (`02-PROMPT-BOILERPLATE.md`)
