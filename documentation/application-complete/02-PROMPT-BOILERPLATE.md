# Prompt pour générer la Boilerplate du Projet

## Comment utiliser ce prompt

1. Ouvrez ChatGPT, Claude, ou tout autre LLM
2. Collez le texte suivant
3. Suivez les instructions du LLM pour créer votre boilerplate
4. Le LLM va vous fournir des scripts à exécuter

---

## 📋 LE PROMPT À COPIER-COLLER

```
Je vais créer une application web complète appelée "NathAnimÂge" pour documenter 
des animations auprès de seniors. 

Voici les détails du projet :

### Description rapide :
- Application web + mobile pour animatrices à domicile
- Permet de documenter rapidement les séances auprès de seniors
- Enregistrement audio + photos + notes vocales/écrites
- IA générative pour transformer les notes en comptes rendus professionnels
- Interface pour les familles (journal de vie)
- Modèle gratuit jusqu'à 5 seniors, puis 15€/mois

### Stack technique requis :

**Frontend :**
- React + TypeScript
- React Native (via Expo) pour accès mobile
- Redux Toolkit pour gestion d'état
- Axios pour appels API
- Tailwind CSS pour styling web
- React Navigation pour navigation mobile
- UI components customisées

**Backend :**
- Python 3.11+
- FastAPI
- PostgreSQL (base de données)
- Redis (cache sessions)
- Whisper API (OpenAI) pour transcription audio
- Claude/GPT-4 API pour génération de texte
- AWS S3 pour stockage fichiers
- JWT pour authentification
- SQLAlchemy ORM

**Infrastructure & Outils :**
- Git + GitHub
- Docker pour conteneurisation
- pytest pour tests backend
- ESLint + Prettier pour code quality frontend
- Environment variables gérées avec .env

### Structure du projet souhaité :

```
nathanimage/
├── frontend/                    # Code React/React Native
│   ├── src/
│   │   ├── components/         # Composants React réutilisables
│   │   ├── pages/              # Pages de l'app
│   │   ├── store/              # Redux slices et configuration
│   │   ├── services/           # Services API (axios)
│   │   ├── hooks/              # Custom React hooks
│   │   ├── utils/              # Utilitaires
│   │   ├── styles/             # Fichiers CSS/Tailwind
│   │   └── types/              # Types TypeScript
│   ├── public/                 # Assets statiques
│   ├── package.json
│   ├── tsconfig.json
│   ├── tailwind.config.js
│   ├── .env.example
│   └── README.md
│
├── backend/                     # Code Python FastAPI
│   ├── app/
│   │   ├── main.py            # Point d'entrée FastAPI
│   │   ├── config.py          # Configuration globale
│   │   ├── dependencies.py    # Dépendances injection
│   │   ├── models/            # Modèles SQLAlchemy
│   │   ├── schemas/           # Pydantic schemas (validation)
│   │   ├── routes/            # Endpoints API
│   │   ├── services/          # Logique métier
│   │   ├── auth/              # Authentification JWT
│   │   ├── ai/                # Intégration IA (Whisper, Claude)
│   │   ├── storage/           # Gestion S3
│   │   ├── database/          # Configuration DB
│   │   └── utils/             # Utilitaires
│   ├── tests/                 # Tests pytest
│   ├── requirements.txt       # Dépendances Python
│   ├── Dockerfile
│   ├── .env.example
│   ├── alembic/              # Migrations base de données
│   └── README.md
│
├── docker-compose.yml         # Stack Docker locale
├── .gitignore
├── .env.example
└── README.md (racine)

```

### Fonctionnalités de base attendues :

**Phase 1 - MVP :**
1. Authentification (sign up, login, logout)
2. Gestion des seniors (CRUD : créer, lire, mettre à jour, supprimer)
3. Créer/lancer une séance
4. Enregistrer audio (avec permission microphone)
5. Prendre des photos (avec permission caméra)
6. Prendre des notes texte
7. Endpoint pour générer compte rendu via IA
8. Dashboard simple affichant liste des séances

**Phase 2 - Avancé :**
1. Partage avec familles (avec permissions)
2. Journal de vie pour famille
3. Système de facturation (gratuit/payant)
4. Système de notifications
5. Analytics basique

### Variables d'environnement minimales :

Backend :
- DATABASE_URL
- OPENAI_API_KEY
- ANTHROPIC_API_KEY
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_S3_BUCKET_NAME
- SECRET_KEY (pour JWT)
- ENVIRONMENT (dev, staging, prod)

Frontend :
- REACT_APP_API_URL
- REACT_APP_ENVIRONMENT

### Points importants :

1. Authentification JWT côté backend obligatoire
2. Validation Pydantic côté backend pour toutes les inputs
3. CORS bien configuré (frontend vers backend)
4. Gestion des erreurs cohérente (format JSON standard)
5. Logging structuré
6. Tests unitaires pour backend
7. Documentation API (Swagger auto-généré par FastAPI)

### Demande :

Génère-moi :
1. Une structure complète de répertoires avec les fichiers clés
2. Les fichiers de configuration (package.json, tsconfig.json, requirements.txt, docker-compose.yml, etc.)
3. Les fichiers .env.example
4. Un main.py (FastAPI) de base avec les middlewares essentiels
5. Un index.tsx (React) de base avec Redux Provider
6. Les schémas Pydantic principaux (User, Senior, Session, Report)
7. Les modèles SQLAlchemy principaux
8. Les routes API de base (auth, seniors, sessions)
9. Un README détaillé pour setup et lancement
10. Les scripts de démarrage (frontend, backend, local)

Format de réponse :
- Affiche chaque fichier avec le chemin complet
- Contenu intégral pour chaque fichier
- Explique le rôle de chaque fichier
- Indique les prochaines étapes après génération

Merci de générer la boilerplate complète !
```

---

## Après avoir reçu la boilerplate

Le LLM va vous fournir une structure complète. Vous devrez alors :

1. **Créer le répertoire** : `mkdir nathanimage && cd nathanimage`
2. **Copier les fichiers** fournis par le LLM
3. **Installer les dépendances** :
   ```bash
   # Frontend
   cd frontend && npm install
   
   # Backend
   cd ../backend && pip install -r requirements.txt
   ```
4. **Configurer .env** : Copier `.env.example` en `.env` et remplir les valeurs

---

## 💡 Conseils de rédaction du prompt

Si le LLM génère quelque chose que vous n'aimez pas :

- **Trop de fichiers ?** Demandez : "Réduis la structure, je veux juste l'essentiel"
- **Manque de commentaires ?** Demandez : "Ajoute des commentaires explicatifs dans le code"
- **Trop simple ?** Demandez : "Ajoute plus de validation, d'error handling, de tests"
- **Besoin de détails ?** Demandez : "Explique chaque fichier ligne par ligne"

---

## 🔗 Lien vers le guide d'architecture

👉 **Voir aussi : `03-ARCHITECTURE-GUIDE.md`** pour comprendre en détail comment les briques s'assemblent
