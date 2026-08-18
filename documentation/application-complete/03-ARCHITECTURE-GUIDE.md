# 📐 Guide Complet de l'Architecture NathAnimÂge

## Vue d'ensemble

```
┌─────────────────────────────────────────────────────────────────────┐
│                         UTILISATEURS                                │
│   Animatrice (Web)          │           Famille (Web + Mobile)      │
└─────────────────────────────────────────────────────────────────────┘
                               ↓
┌─────────────────────────────────────────────────────────────────────┐
│                    FRONTEND (React + TypeScript)                    │
│  ┌──────────────┬──────────────────┬──────────────────┬────────────┐
│  │ Pages        │ Composants       │ Redux Store      │ Services   │
│  │              │                  │                  │            │
│  │ • Login      │ • Forms          │ • Auth slice     │ • API      │
│  │ • Sessions   │ • Photo Gallery  │ • Sessions slice │ • Upload   │
│  │ • Reports    │ • AudioRecorder  │ • Seniors slice  │ • Download │
│  │ • Seniors    │ • DatePicker     │ • Reports slice  │            │
│  │ • Family     │ • Modals         │                  │            │
│  └──────────────┴──────────────────┴──────────────────┴────────────┘
                               ↓ (Axios HTTP)
┌─────────────────────────────────────────────────────────────────────┐
│                  BACKEND API (Python + FastAPI)                     │
│  ┌──────────────┬──────────────────┬──────────────────┬────────────┐
│  │ Routes       │ Business Logic   │ Database Ops     │ External   │
│  │              │                  │                  │            │
│  │ • /auth      │ • Validation     │ • SQLAlchemy ORM │ • Whisper  │
│  │ • /seniors   │ • Auth logic     │ • PostgreSQL     │ • Claude   │
│  │ • /sessions  │ • AI pipeline    │ • Migrations     │ • S3       │
│  │ • /reports   │ • File handling  │ • Transactions   │            │
│  │ • /users     │ • Pricing logic  │                  │            │
│  └──────────────┴──────────────────┴──────────────────┴────────────┘
                               ↓
┌─────────────────────────────────────────────────────────────────────┐
│                      INFRASTRUCTURE                                 │
│  ┌─────────────────┬─────────────────┬──────────────────────────────┐
│  │ PostgreSQL      │ Redis Cache     │ External Services            │
│  │ (Data Storage)  │ (Sessions)      │                              │
│  │                 │                 │ • OpenAI Whisper (audio→text)│
│  │ • Users         │ • Auth tokens   │ • Claude/GPT-4 (AI gen)      │
│  │ • Seniors       │ • Cache data    │ • AWS S3 (file storage)      │
│  │ • Sessions      │                 │                              │
│  │ • Reports       │                 │                              │
│  │ • Photos        │                 │                              │
│  │ • Audio files   │                 │                              │
│  └─────────────────┴─────────────────┴──────────────────────────────┘
```

---

## 1️⃣ FRONTEND - React + TypeScript

### 1.1 Structure des dossiers

```
frontend/src/
├── components/          # Composants réutilisables
│   ├── atoms/           # Petits blocs (buttons, inputs, badges)
│   ├── molecules/       # Combinaisons (forms, cards)
│   └── organisms/       # Sections complètes (headers, modals)
│
├── pages/              # Pages/écrans de l'app
│   ├── auth/           # Login, signup
│   ├── dashboard/      # Accueil
│   ├── sessions/       # Créer/voir sessions
│   ├── seniors/        # Gérer seniors
│   ├── reports/        # Voir comptes rendus
│   └── family/         # Journal famille
│
├── store/              # Redux (gestion d'état)
│   ├── slices/         # Données + actions
│   │   ├── authSlice.ts       # User, login state
│   │   ├── sessionsSlice.ts   # Sessions, recordings
│   │   ├── seniors Slice.ts   # Liste seniors
│   │   └── reportsSlice.ts    # Comptes rendus
│   └── hooks.ts         # Hooks Redux customisés
│
├── services/           # Appels API
│   ├── api.ts          # Configuration Axios
│   ├── authService.ts  # Login, signup, logout
│   ├── sessionsService.ts
│   ├── seniorsService.ts
│   └── reportsService.ts
│
├── hooks/              # Logic réutilisable
│   ├── useAuth.ts      # Authentification
│   ├── useRecording.ts # Enregistrement audio
│   ├── useCamera.ts    # Prise de photos
│   └── useFetch.ts     # Fetch de données
│
├── utils/              # Fonctions utilitaires
│   ├── formatters.ts   # Format dates, nombres
│   ├── validators.ts   # Validation formulaires
│   └── storage.ts      # LocalStorage
│
├── types/              # Types TypeScript
│   ├── auth.ts
│   ├── sessions.ts
│   ├── seniors.ts
│   └── reports.ts
│
└── styles/             # CSS/Tailwind
    ├── globals.css
    ├── variables.css
    └── tailwind.config.js
```

### 1.2 Flux de données (Redux)

```
Utilisateur interagit
        ↓
Appel API (service)
        ↓
Dispatch action Redux
        ↓
Reducer met à jour le store
        ↓
Composants abonnés au store reçoivent nouvelles données
        ↓
UI se met à jour automatiquement
```

**Exemple concret : créer une session**

```typescript
// 1. Utilisateur clique sur "Nouvelle séance"
<button onClick={() => dispatch(createSession(seniorId))}>

// 2. Service appelle l'API
// frontend/services/sessionsService.ts
export function createSession(seniorId) {
  return api.post('/sessions', { senior_id: seniorId })
}

// 3. Redux reçoit et stocke
// frontend/store/slices/sessionsSlice.ts
createSession: (state, action) => {
  state.currentSession = action.payload
}

// 4. UI se met à jour
// frontend/pages/sessions/RecordingPage.tsx
const { currentSession } = useSelector(state => state.sessions)
return <div>{currentSession.id}</div>
```

### 1.3 Communication avec le Backend

**Tous les appels frontend → backend passent par Axios**

```typescript
// frontend/services/api.ts
import axios from 'axios'

const api = axios.create({
  baseURL: process.env.REACT_APP_API_URL || 'http://localhost:8000'
})

// Ajouter le token JWT à chaque requête
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token')
  if (token) {
    config.headers.Authorization = `Bearer ${token}`
  }
  return config
})

export default api
```

### 1.4 Points clés du Frontend

✅ **À faire** :
- Stocker le JWT en localStorage
- Valider les formulaires avant d'envoyer
- Afficher les erreurs à l'utilisateur
- Compresser les photos avant upload
- Gérer les états de chargement (loading, error, success)

❌ **À éviter** :
- Appeler l'API directement (passer par services)
- Stocker trop d'état local (utiliser Redux)
- Mettre des secrets en .env (utiliser .env.local)
- Oublier le CORS

---

## 2️⃣ BACKEND - Python + FastAPI

### 2.1 Structure des dossiers

```
backend/
├── app/
│   ├── main.py              # Point d'entrée FastAPI
│   ├── config.py            # Configuration globale
│   ├── dependencies.py      # Dépendances injection
│   │
│   ├── models/              # SQLAlchemy ORM (représentation DB)
│   │   ├── user.py          # Utilisateurs (animatrices)
│   │   ├── senior.py        # Seniors
│   │   ├── session.py       # Séances
│   │   ├── report.py        # Comptes rendus
│   │   └── photo.py         # Photos
│   │
│   ├── schemas/             # Pydantic (validation requêtes/réponses)
│   │   ├── auth.py          # LoginRequest, SignupRequest
│   │   ├── senior.py        # SeniorCreate, SeniorRead
│   │   ├── session.py       # SessionCreate, SessionRead
│   │   └── report.py        # ReportRead, ReportGenerate
│   │
│   ├── routes/              # Endpoints API
│   │   ├── auth.py          # /auth/login, /auth/signup
│   │   ├── seniors.py       # /seniors (CRUD)
│   │   ├── sessions.py      # /sessions (CRUD)
│   │   ├── reports.py       # /reports (génération IA)
│   │   └── photos.py        # /photos (upload)
│   │
│   ├── services/            # Logique métier
│   │   ├── auth_service.py  # Authentification JWT
│   │   ├── ai_service.py    # Appels Whisper + Claude
│   │   ├── storage_service.py  # Gestion S3
│   │   └── pricing_service.py  # Vérification gratuit/payant
│   │
│   ├── database/            # Configuration DB
│   │   ├── database.py      # SQLAlchemy setup
│   │   ├── session.py       # DB session
│   │   └── base.py          # Base class pour models
│   │
│   ├── auth/                # Authentification
│   │   └── jwt.py           # JWT token generation/validation
│   │
│   └── utils/               # Utilitaires
│       ├── logger.py
│       └── validators.py
│
├── tests/                   # Tests pytest
│   ├── test_auth.py
│   ├── test_sessions.py
│   └── conftest.py
│
├── alembic/                 # Migrations base de données
│   └── versions/
│
├── requirements.txt         # Dépendances Python
├── .env.example
├── Dockerfile
└── README.md
```

### 2.2 Flux des requêtes HTTP

```
1. Client envoie POST /sessions
         ↓
2. FastAPI reçoit et valide avec Pydantic (schemas)
         ↓
3. Route appelle service métier
         ↓
4. Service crée/modifie objet SQLAlchemy (model)
         ↓
5. Base de données sauvegarde (PostgreSQL)
         ↓
6. Response converti en JSON et envoyé au client
```

**Exemple concret : créer une session**

```python
# backend/app/routes/sessions.py
from fastapi import APIRouter, Depends
from sqlalchemy.orm import Session

router = APIRouter()

@router.post("/sessions")
def create_session(
    session_data: SessionCreate,  # Validé par Pydantic
    db: Session = Depends(get_db),  # Injection DB
    current_user: User = Depends(get_current_user)  # Auth
):
    # Créer l'objet model SQLAlchemy
    new_session = SessionModel(
        senior_id=session_data.senior_id,
        animator_id=current_user.id,
        status="in_progress"
    )
    
    # Sauvegarder en DB
    db.add(new_session)
    db.commit()
    db.refresh(new_session)
    
    # Retourner au client
    return SessionRead.from_orm(new_session)
```

### 2.3 Les services clés

#### 🔐 Authentification (auth_service.py)

```python
def create_access_token(user_id: int):
    # Crée un JWT qui prouve l'identité
    # Valable 24h
    # Contient l'user_id encodé
    
def verify_access_token(token: str):
    # Vérifie que le token est valide
    # Decode et retourne l'user_id
```

#### 🤖 IA (ai_service.py)

```python
def transcribe_audio(audio_file_path):
    # Envoie à Whisper API
    # Reçoit le texte transcrit
    return text

def generate_report(notes, transcription, photos_descriptions):
    # Envoie tout à Claude/GPT
    # Claude rédige un beau compte rendu
    # Retourne le rapport généré
    return professional_report
```

#### 💾 Stockage (storage_service.py)

```python
def upload_photo_to_s3(file):
    # Compresse la photo
    # Upload à AWS S3
    # Retourne l'URL publique

def download_from_s3(url):
    # Récupère un fichier depuis S3
```

#### 💰 Pricing (pricing_service.py)

```python
def can_create_senior(user_id):
    # Compte combien de seniors l'animatrice a
    # Si < 5 : gratuit, return True
    # Si >= 5 et payant : return True
    # Sinon : return False (besoin d'upgrade)
```

### 2.4 Points clés du Backend

✅ **À faire** :
- Valider TOUTES les entrées avec Pydantic
- Vérifier que l'utilisateur a les permissions
- Utiliser les transactions DB
- Logger tout (erreurs, actions)
- Gérer les erreurs proprement

❌ **À éviter** :
- Faire confiance aux données du client
- Appeler l'API IA directement (faire passer par service)
- Oublier les validations
- Stocker les secrets en dur (utiliser .env)

---

## 3️⃣ LA COMMUNICATION FRONTEND ↔ BACKEND

### 3.1 Exemple complet : générer un compte rendu

#### **Étape 1 : Frontend prépare les données**

```typescript
// frontend/pages/reports/GenerateReport.tsx
const handleGenerateReport = async () => {
  const reportData = {
    session_id: currentSession.id,
    notes: userNotes,
    audio_file_urls: [audioUrls...],
    photo_urls: [photoUrls...],
  }
  
  dispatch(generateReport(reportData))
}
```

#### **Étape 2 : Frontend envoie au backend**

```typescript
// frontend/services/reportsService.ts
export function generateReport(data) {
  return api.post('/reports/generate', data, {
    headers: {
      'Authorization': `Bearer ${token}`  // JWT
    }
  })
}
```

#### **Étape 3 : Backend reçoit**

```python
# backend/app/routes/reports.py
@router.post("/reports/generate")
def generate_report(
    report_request: ReportGenerateRequest,
    current_user: User = Depends(get_current_user)
):
    session = db.query(SessionModel).filter(
        SessionModel.id == report_request.session_id
    ).first()
```

#### **Étape 4 : Backend utilise l'IA**

```python
# backend/app/services/ai_service.py
def generate_report(notes, audio_urls, photo_urls):
    # 1. Transcribe les audios
    audio_texts = [transcribe_audio(url) for url in audio_urls]
    
    # 2. Envoie tout à Claude
    prompt = f"""
    Génère un compte rendu professionnel:
    Notes: {notes}
    Audios transcrits: {audio_texts}
    Photos (description): {photo_urls}
    """
    
    report_text = call_claude(prompt)
    return report_text
```

#### **Étape 5 : Backend sauvegarde en DB**

```python
new_report = ReportModel(
    session_id=session.id,
    content=report_text,
    created_at=datetime.now()
)
db.add(new_report)
db.commit()
```

#### **Étape 6 : Backend retourne au frontend**

```python
return ReportRead(
    id=new_report.id,
    content=new_report.content,
    created_at=new_report.created_at
)
```

#### **Étape 7 : Frontend reçoit et affiche**

```typescript
// Redux met à jour
state.currentReport = response.data

// UI affiche
const { currentReport } = useSelector(state => state.reports)
return <div>{currentReport.content}</div>
```

---

## 4️⃣ BASE DE DONNÉES - PostgreSQL

### 4.1 Schéma principal

```sql
-- Utilisateurs (animatrices)
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    name VARCHAR(255),
    created_at TIMESTAMP DEFAULT NOW(),
    subscription_status ENUM ('free', 'premium'),  -- Modèle économique
    is_active BOOLEAN DEFAULT TRUE
);

-- Seniors (personnes âgées)
CREATE TABLE seniors (
    id SERIAL PRIMARY KEY,
    animator_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    date_of_birth DATE,
    preferences TEXT,  -- Texte libre
    created_at TIMESTAMP DEFAULT NOW()
);

-- Séances (documentations)
CREATE TABLE sessions (
    id SERIAL PRIMARY KEY,
    senior_id INTEGER REFERENCES seniors(id) ON DELETE CASCADE,
    animator_id INTEGER REFERENCES users(id),
    status ENUM ('in_progress', 'completed'),
    started_at TIMESTAMP DEFAULT NOW(),
    ended_at TIMESTAMP,
    notes TEXT
);

-- Comptes rendus (générés par IA)
CREATE TABLE reports (
    id SERIAL PRIMARY KEY,
    session_id INTEGER REFERENCES sessions(id) ON DELETE CASCADE,
    content TEXT NOT NULL,  -- Texte généré
    created_at TIMESTAMP DEFAULT NOW(),
    shared_with_family BOOLEAN DEFAULT FALSE
);

-- Photos
CREATE TABLE photos (
    id SERIAL PRIMARY KEY,
    session_id INTEGER REFERENCES sessions(id) ON DELETE CASCADE,
    s3_url VARCHAR(255),  -- Lien S3
    uploaded_at TIMESTAMP DEFAULT NOW()
);

-- Enregistrements audio
CREATE TABLE audio_recordings (
    id SERIAL PRIMARY KEY,
    session_id INTEGER REFERENCES sessions(id) ON DELETE CASCADE,
    s3_url VARCHAR(255),
    transcription TEXT,  -- Texte transcrit par Whisper
    created_at TIMESTAMP DEFAULT NOW()
);

-- Permissions famille (qui voit quoi)
CREATE TABLE family_access (
    id SERIAL PRIMARY KEY,
    senior_id INTEGER REFERENCES seniors(id),
    family_member_id INTEGER REFERENCES users(id),
    access_level ENUM ('view_only', 'can_comment'),
    granted_at TIMESTAMP DEFAULT NOW()
);
```

### 4.2 Relations principales

```
users (1) ──→ (many) seniors
users (1) ──→ (many) sessions
seniors (1) ──→ (many) sessions
sessions (1) ──→ (many) reports
sessions (1) ──→ (many) photos
sessions (1) ──→ (many) audio_recordings
```

---

## 5️⃣ SERVICES EXTERNES

### 5.1 Whisper API (Transcription audio)

```
App → AudioFile → Whisper → Text → App
```

**Coût** : $0.006 par minute d'audio

**Exemple** :
- Enregistrement de 5 min → $0.03

### 5.2 Claude/GPT-4 (Génération IA)

```
App → Notes + Texte + Descriptions → Claude → Rapport professionnel → App
```

**Coût** : Par tokens (mots)
- Claude : ~$0.01/1000 tokens
- Rapport typique (500 tokens) → ~$0.005

### 5.3 AWS S3 (Stockage)

```
App → Photo/Audio → S3 → URL publique → App
```

**Coût** : 
- Gratuit jusqu'à 5GB
- Puis $0.023 par GB/mois
- Transfert de données : ~$0.09 par GB

---

## 6️⃣ VARIABLES D'ENVIRONNEMENT

### Backend (.env)

```
# Base de données
DATABASE_URL=postgresql://user:password@localhost:5432/nathanimage

# IA
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...

# Stockage fichiers
AWS_ACCESS_KEY_ID=AKIA...
AWS_SECRET_ACCESS_KEY=...
AWS_S3_BUCKET_NAME=nathanimage-bucket

# Authentification
SECRET_KEY=random_very_long_secret_key_here

# Environment
ENVIRONMENT=development
DEBUG=True
```

### Frontend (.env.local)

```
REACT_APP_API_URL=http://localhost:8000
REACT_APP_ENVIRONMENT=development
```

---

## 7️⃣ WORKFLOW COMPLET : DU DÉBUT À LA FIN

### 📱 Animatrice documente

```
1. Se connecte
   └─→ Backend valide email + password
   └─→ Backend crée JWT
   └─→ Frontend stocke JWT

2. Crée une séance
   └─→ Choisit senior
   └─→ Frontend: POST /sessions
   └─→ Backend crée SessionModel
   └─→ Frontend stocke session_id

3. Pendant la séance
   - Prend des photos
     └─→ Compresse
     └─→ Upload à S3
     └─→ Sauvegarde URL en DB
   
   - Enregistre audio
     └─→ Upload à S3
     └─→ Sauvegarde URL en DB
   
   - Écrit des notes
     └─→ Sauvegarde localement

4. Termine et génère rapport
   └─→ Frontend: POST /reports/generate
   └─→ Backend récupère tous les fichiers
   └─→ Transcribe audio (Whisper)
   └─→ Envoie tout à Claude
   └─→ Claude génère rapport professionnel
   └─→ Sauvegarde rapport en DB
   └─→ Retourne au frontend
   └─→ Animatrice vérifie et peut modifier
```

### 👨‍👩‍👧 Famille consulte

```
1. Se connecte (accès famille)
2. Voit journal chronologique
   - Dates des séances
   - Comptes rendus
   - Photos
   - Audio (avec description)
3. Peut laisser des commentaires
```

---

## 8️⃣ POINTS CRITIQUES POUR LA SÉCURITÉ

### 🔒 Authentification

```
✅ Tous les endpoints protégés par JWT
✅ Passwords hashés en DB (jamais en clair)
✅ Tokens stockés en localStorage (frontend)
✅ CORS bien configuré
```

### 🔐 Autorisation

```
✅ Animatrice ne voit QUE ses seniors
✅ Famille ne voit QUE les seniors accessibles
✅ Vérifier les permissions sur chaque requête
```

### 🛡️ Données sensibles

```
✅ Chiffrer audio/photos en transit (HTTPS)
✅ Pas de données en logs
✅ S3 avec permissions strictes
```

---

## 📚 Prochaines étapes

1. ✅ Lire le glossaire ([04-GLOSSAIRE-TECHNOS.md](04-GLOSSAIRE-TECHNOS.md))
2. ✅ Utiliser le prompt pour générer la boilerplate ([02-PROMPT-BOILERPLATE.md](02-PROMPT-BOILERPLATE.md))
3. ✅ Configurer l'environnement local
4. ✅ Tester chaque brique indépendamment
5. ✅ Intégrer progressivement
