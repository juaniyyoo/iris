# 📖 Glossaire Complet - Toutes les Technologies

Table des matières :
- [Frontend](#frontend)
- [Backend](#backend)
- [Bases de données](#bases-de-données)
- [Services cloud](#services-cloud)
- [Outils et processus](#outils-et-processus)
- [Concepts généraux](#concepts-généraux)

---

## FRONTEND

### ⚛️ React
**Qu'est-ce que c'est ?**
Bibliothèque JavaScript pour construire des interfaces utilisateur interactives.

**En analogie simple :**
Imagine un système de LEGO. Au lieu de construire l'interface à chaque fois, tu crées des blocs réutilisables. React gère automatiquement ce qui change sur l'écran.

**Pourquoi l'utiliser ?**
- Facile à apprendre
- Code réutilisable (composants)
- Très populaire (beaucoup de ressources)
- Performance optimisée

**Exemple :**
```jsx
function Welcome() {
  return <h1>Bonjour, animatrice!</h1>
}

// Tu peux réutiliser ce composant partout
<Welcome />
```

**Site officiel** : https://react.dev

---

### 📱 React Native
**Qu'est-ce que c'est ?**
Version de React qui crée des apps mobiles (iOS et Android) en utilisant la même syntaxe que React pour le web.

**En analogie simple :**
Au lieu d'écrire du code différent pour iPhone et Android, tu écris une fois avec React Native et ça fonctionne sur les deux.

**Pourquoi l'utiliser ?**
- Un seul codebase pour 2 plateformes
- Plus rapide à développer
- Code partageable avec le web (React)

**Important :**
React Native n'est PAS un navigateur. Les composants sont natifs (vrais contrôles iOS/Android).

**Site officiel** : https://reactnative.dev

---

### 🚀 Expo
**Qu'est-ce que c'est ?**
Outil qui simplifie le développement d'apps React Native. Te permet de voir les changements en temps réel sur ton téléphone.

**En analogie simple :**
Sans Expo, tu devrais compiler ton app chaque fois. Expo te laisse voir les changements immédiatement en scannant un QR code.

**Avantages principaux :**
- Développement plus rapide
- Pas besoin d'Android Studio ou Xcode au début
- Accès facile aux capteurs (caméra, microphone, etc.)
- Déploiement simplifié

**Exemple workflow :**
```bash
npm start                # Lance le serveur Expo
# Scanne le QR code avec ton téléphone
# Les changements s'affichent immédiatement
```

**Site officiel** : https://docs.expo.dev

---

### 🎨 TypeScript
**Qu'est-ce que c'est ?**
JavaScript + système de types. Ça veut dire que tu dis à l'avance "ce paramètre est un nombre", et TS te dit si tu fais une erreur.

**En analogie simple :**
C'est comme avoir un copilot qui te signale les erreurs AVANT de lancer le code.

**Exemple :**
```typescript
// Erreur ! On dit que age est un nombre, mais on envoie du texte
function canAnimateThisSenior(age: number): boolean {
  return age >= 18
}

canAnimateThisSenior("vingt")  // ❌ TypeScript crie : "c'est pas un nombre!"
canAnimateThisSenior(20)        // ✅ OK
```

**Avantages :**
- Erreurs attrapées avant runtime
- Meilleure autocomplétion dans l'éditeur
- Code plus maintenable

**Site officiel** : https://www.typescriptlang.org

---

### 🎯 Redux Toolkit
**Qu'est-ce que c'est ?**
Système de gestion d'état centralisé. Au lieu de passer les données de composant en composant, tu les mets dans un "magasin" central.

**En analogie simple :**
Imagine que tu as un classeur central où tout le monde peut aller chercher les informations. Au lieu de passer des papiers de personne en personne, tout est accessible au même endroit.

**Sans Redux (problématique) :**
```
Parent comp → Child comp → Grandchild comp
C'est quoi, "grandchild" reçoit directement des données du parent 5 niveaux plus haut. Compliqué!
```

**Avec Redux :**
```
Grandchild comp → "Je dois récupérer userID" → Redux Store → Voilà!
```

**Concepts clés :**
- **Store** : L'endroit central qui stocke tout
- **Slice** : Un morceau du store (ex: slice "auth", slice "sessions")
- **Action** : Une instruction de changement (ex: "connecte cet utilisateur")
- **Reducer** : Fonction qui dit comment le store change (ex: "si action=login, ajoute l'user au store")

**Exemple :**
```typescript
// 1. Créer un slice (morceau du store)
const authSlice = createSlice({
  name: 'auth',
  initialState: { user: null },
  reducers: {
    setUser: (state, action) => {
      state.user = action.payload
    }
  }
})

// 2. Dispatcher une action
dispatch(authSlice.actions.setUser({ id: 1, email: 'anna@xxx' }))

// 3. Récupérer les données partout
const user = useSelector(state => state.auth.user)
```

**Pourquoi Redux Toolkit ?**
- Beaucoup plus simple que Redux classique
- Moins de code à écrire
- Meilleures performances

**Site officiel** : https://redux-toolkit.js.org

---

### 🌐 Axios
**Qu'est-ce que c'est ?**
Bibliothèque pour faire des requêtes HTTP (parler à l'API backend).

**En analogie simple :**
C'est comme un standardiste qui fait les appels téléphoniques à l'API pour toi. "Hé API, j'ai besoin des données du senior 5, s'il te plaît".

**Sans Axios (compliqué) :**
```javascript
// Code verbeux avec fetch natif
fetch('http://api.xxx/seniors/5')
  .then(res => res.json())
  .then(data => console.log(data))
```

**Avec Axios (simple) :**
```javascript
const response = await api.get('/seniors/5')
console.log(response.data)
```

**Avantages :**
- Syntaxe plus lisible
- Gère les intercepteurs (ajouter le JWT automatiquement)
- Gère les timeouts
- Transformations données

**Configuration classique :**
```typescript
const api = axios.create({
  baseURL: 'http://localhost:8000'
})

// Ajouter le JWT automatiquement à chaque requête
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token')
  if (token) {
    config.headers.Authorization = `Bearer ${token}`
  }
  return config
})
```

**Site officiel** : https://axios-http.com

---

### 🎨 Tailwind CSS
**Qu'est-ce que c'est ?**
Framework CSS qui donne des classes pré-faites pour styliser rapidement.

**En analogie simple :**
Au lieu de écrire du CSS custom, tu utilises des classes prêtes à l'emploi.

**Sans Tailwind (long) :**
```css
.button {
  padding: 12px 24px;
  background-color: #3b82f6;
  color: white;
  border-radius: 8px;
  font-weight: 600;
}
```

**Avec Tailwind (rapide) :**
```jsx
<button className="px-6 py-3 bg-blue-500 text-white rounded-lg font-semibold">
  Cliquez-moi
</button>
```

**Avantages :**
- Très rapide à développer
- Design cohérent
- Pas de fichiers CSS séparés (tout dans le JSX)
- Responsive design facile

**Site officiel** : https://tailwindcss.com

---

### 🧭 React Navigation
**Qu'est-ce que c'est ?**
Système pour naviguer entre les écrans dans une app mobile.

**En analogie simple :**
C'est le système de menu de ton app. Tu cliques sur "Voir mes seniors", tu vas vers cette page. Tu cliques "Retour", tu reviens.

**Types de navigation :**
- **Stack** : Comme une pile de cartes (tu peux revenir)
- **Tab** : Menu en bas avec plusieurs onglets
- **Drawer** : Menu latéral (glisse depuis la gauche)

**Exemple :**
```typescript
<NavigationContainer>
  <Stack.Navigator>
    <Stack.Screen name="Home" component={HomeScreen} />
    <Stack.Screen name="Sessions" component={SessionsScreen} />
  </Stack.Navigator>
</NavigationContainer>
```

**Site officiel** : https://reactnavigation.org

---

## BACKEND

### 🐍 Python
**Qu'est-ce que c'est ?**
Langage de programmation connu pour être lisible et simple.

**En analogie simple :**
Si JavaScript c'est "le langage des sites web", Python c'est "le langage des calculs et de la logique métier". Beaucoup utilisé pour l'IA, les données, etc.

**Pourquoi pour un débutant ?**
- Syntaxe très lisible (ressemble presque à de l'anglais)
- Énorme communauté
- Tonnes de librairies disponibles
- Parfait pour backend

**Exemple simple :**
```python
# Très lisible, pas besoin de ; ou de {} 
def verify_animator_credentials(email, password):
    if email and password:
        return True
    return False

result = verify_animator_credentials("anna@xxx.fr", "password123")
print(result)  # True
```

**Site officiel** : https://www.python.org

---

### ⚡ FastAPI
**Qu'est-ce que c'est ?**
Framework Python ultra-rapide pour créer des APIs REST.

**En analogie simple :**
C'est le "serveur" de ton app. FastAPI reçoit les demandes du frontend et envoie les réponses.

```
Frontend: "Hé, donne-moi les infos du senior 5"
FastAPI: (va chercher en base de données)
FastAPI: "Voilà: nom=Jean, âge=82"
```

**Sans FastAPI (long) :**
Beaucoup de code pour configurer un serveur HTTP.

**Avec FastAPI (simple) :**
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/seniors/{senior_id}")
def get_senior(senior_id: int):
    # Va chercher le senior 
    return {"id": senior_id, "name": "Jean"}

# C'est tout ! C'est déjà un serveur fonctionnel
```

**Avantages :**
- **Auto-documentation** : FastAPI génère une doc interactive
- **Validation automatique** : Pydantic valide les données
- **Performance** : Aussi rapide que Node.js
- **Async** : Peut gérer plusieurs requêtes simultanées

**Site officiel** : https://fastapi.tiangolo.com

---

### 🗄️ SQLAlchemy
**Qu'est-ce que c'est ?**
ORM (Object-Relational Mapping). Ça signifie "au lieu d'écrire du SQL, tu écris du Python, et SQLAlchemy fait la traduction".

**En analogie simple :**
La base de données c'est comme un tableau Excel. SQLAlchemy crée une représentation Python de ce tableau.

**Sans SQLAlchemy (écrire du SQL) :**
```sql
SELECT * FROM seniors WHERE animator_id = 5
```

**Avec SQLAlchemy (écrire du Python) :**
```python
seniors = db.query(Senior).filter(Senior.animator_id == 5).all()
```

**Modèle SQLAlchemy :**
```python
class Senior(Base):
    __tablename__ = "seniors"
    
    id = Column(Integer, primary_key=True)
    name = Column(String)
    animator_id = Column(Integer, ForeignKey("users.id"))
    date_of_birth = Column(Date)
    created_at = Column(DateTime, default=datetime.utcnow)
```

**Avantages :**
- Pas d'SQL à écrire (plus sûr contre injections)
- Code Python réutilisable
- Migrations faciles (Alembic)

**Site officiel** : https://www.sqlalchemy.org

---

### ✔️ Pydantic
**Qu'est-ce que c'est ?**
Validation de données en Python. Avant de traiter une requête, Pydantic vérifie que les données sont correctes.

**En analogie simple :**
Un gardien à la porte qui dit "es-tu sûr que tu es animator_id qui est un nombre ? Pas du texte ?".

**Sans Pydantic (pas sûr) :**
```python
@app.post("/sessions")
def create_session(data):
    # data est un dict Python, on ne sait pas si c'est valide
    session = Session(animator_id=data.get('animator_id'))  # Et si c'est du texte?
```

**Avec Pydantic (sûr) :**
```python
class SessionCreate(BaseModel):
    animator_id: int  # Doit être un nombre
    senior_id: int
    notes: str

@app.post("/sessions")
def create_session(data: SessionCreate):  # Pydantic valide automatiquement
    # On SAIT que data.animator_id est un int
    session = Session(animator_id=data.animator_id)
```

**Si les données ne sont pas valides :**
FastAPI retourne automatiquement une erreur 422 au frontend.

**Site officiel** : https://docs.pydantic.dev

---

## BASES DE DONNÉES

### 🐘 PostgreSQL
**Qu'est-ce que c'est ?**
Base de données relationnelle. C'est là où tu stockes toutes les données de l'app (utilisateurs, seniors, séances, rapports, etc.).

**En analogie simple :**
C'est un tableau Excel ultra-puissant qui :
- Peut gérer des millions de lignes
- Vérifie l'intégrité des données
- Peut faire des requêtes complexes rapidement

**Structure :**
```
PostgreSQL = Classeur
  ├── Table "users"
  │   ├── id | email | password_hash | name
  │   ├── 1 | anna@xxx | xxxxx | Anna
  │   └── 2 | jean@xxx | yyyyy | Jean
  │
  ├── Table "seniors"
  │   ├── id | name | animator_id | date_of_birth
  │   ├── 1 | Paul | 1 | 1942-05-15
  │   └── 2 | Marie | 1 | 1950-03-20
```

**Avantages :**
- Open source et gratuit
- Très stable (utilisé par Netflix, Spotify, etc.)
- Puissant (requêtes complexes, transactions)
- Support des relations entre tables (clés étrangères)

**Site officiel** : https://www.postgresql.org

---

### 💾 Redis
**Qu'est-ce que c'est ?**
Cache ultra-rapide. On stocke les données souvent utilisées en mémoire pour y accéder très vite.

**En analogie simple :**
PostgreSQL c'est un grand classeur rempli (lent à chercher). Redis c'est un post-it sur le bureau (accès instantané).

**Exemples d'usage :**
- Stocker les sessions utilisateurs (quién est connecté)
- Cacher les réponses API souvent demandées
- Mettre en queue les jobs (transcription audio)

**Comparaison :**
```
PostgreSQL: "Cherche l'utilisateur 5" → Cherche dans le disque → 10-50ms
Redis: "Cherche l'utilisateur 5" → Regarde la RAM → 0.1-1ms
```

**Important :** Redis ne sauvegarde PAS les données sur le disque (par défaut). Si Redis crash, les données en cache sont perdues. Donc on ne l'utilise que pour du temporaire.

**Site officiel** : https://redis.io

---

## SERVICES CLOUD

### 🤖 OpenAI Whisper
**Qu'est-ce que c'est ?**
Service de transcription audio à texte. Tu envoies un fichier audio, Whisper retourne le texte transcrit.

**En analogie simple :**
Un secrétaire automatique qui écoute et écrit ce qui est dit.

**Comment ça marche :**
```
Fichier audio (mp3) → Whisper API → Texte transcrit
"Bonjour, on a fait un gâteau aujourd'hui..." → "Bonjour, on a fait un gâteau aujourd'hui..."
```

**Avantages :**
- Support de 50+ langues
- Très précis
- Pas cher ($0.006 par minute)

**Exemple :**
```python
import openai

def transcribe_audio(audio_file_path):
    with open(audio_file_path, "rb") as audio_file:
        transcript = openai.Audio.transcribe("whisper-1", audio_file)
    return transcript["text"]

text = transcribe_audio("session_audio.mp3")
print(text)  # "Bonjour, on a fait un gâteau aujourd'hui..."
```

**Site officiel** : https://platform.openai.com/docs/guides/speech-to-text

---

### 🧠 Claude / GPT-4 (IA générative)
**Qu'est-ce que c'est ?**
IA capable de générer du texte cohérent. Tu décris ce que tu veux, elle le génère.

**En analogie simple :**
Un écrivain automatique. Tu lui donnes des notes brutes, il rédige un texte professionnel.

**Exemple pour NathAnimÂge :**
```
INPUT :
- Notes: "Aujourd'hui on a peint des toiles. Jean a adoré."
- Audio transcrit: "Vous ne croirez pas comme c'était cool"
- Photos: (description de 3 photos)

CLAUDE :
"Séance enrichissante du 18/08/2026
Jean a participé avec enthousiasme à une séance de peinture. 
Les activités proposées ont stimulé sa créativité...
[Rapport professionnel généré]"
```

**Différences Claude vs GPT-4 :**
- **Claude** (Anthropic) : Très bon pour la génération, moins cher
- **GPT-4** (OpenAI) : Très polyvalent, un peu plus cher

Pour NathAnimÂge, l'un ou l'autre fonctionne. Claude est recommandé pour la qualité.

**Coûts :**
- Claude: ~$0.01 par 1000 tokens (mots)
- GPT-4: ~$0.03 par 1000 tokens

**Exemple :**
```python
from anthropic import Anthropic

def generate_report(notes, transcription, photos):
    client = Anthropic()
    
    prompt = f"""
    Génère un compte rendu professionnel pour une animation auprès d'une personne âgée.
    
    Notes de l'animatrice: {notes}
    Enregistrement transcrit: {transcription}
    Photos: {photos}
    
    Le compte rendu doit être warm, professionnel, et partageable avec la famille.
    """
    
    message = client.messages.create(
        model="claude-3-sonnet-20240229",
        max_tokens=1024,
        messages=[{"role": "user", "content": prompt}]
    )
    
    return message.content[0].text
```

**Sites officiels :**
- Claude : https://www.anthropic.com/claude
- GPT-4 : https://openai.com/gpt-4

---

### ☁️ AWS S3
**Qu'est-ce que c'est ?**
Service de stockage de fichiers dans le cloud. Tu mets tes photos et audios dans S3, et tu reçois des URLs pour y accéder.

**En analogie simple :**
Un Google Drive gratuit et illimité pour les fichiers de ton app.

**Comment ça marche :**
```
1. Utilisateur prend une photo
2. App envoie la photo à S3
3. S3 retourne une URL (ex: https://s3.amazonaws.com/nathanimage/photos/123.jpg)
4. App sauvegarde cette URL en base de données
5. Frontend affiche la photo en utilisant l'URL
```

**Avantages :**
- Pas de stockage local → plus d'espace sur le serveur
- Scalable (peut accueillir des millions de fichiers)
- CDN intégré (fichiers servis rapidement partout)
- Fiable (redondance, backups)

**Exemple :**
```python
import boto3

s3_client = boto3.client('s3')

def upload_photo_to_s3(file, filename):
    s3_client.upload_fileobj(
        file,
        bucket_name='nathanimage-bucket',
        key=f'photos/{filename}'
    )
    
    url = f"https://nathanimage-bucket.s3.amazonaws.com/photos/{filename}"
    return url

# Utilisation
photo_url = upload_photo_to_s3(photo_file, "senior_5_20260818.jpg")
print(photo_url)  # https://nathanimage-bucket.s3.amazonaws.com/photos/senior_5_20260818.jpg
```

**Coûts (pour petites apps) :**
- Gratuit jusqu'à 5GB
- Puis $0.023 par GB/mois
- Pour la plupart des petits projets : quasi gratuit

**Site officiel** : https://aws.amazon.com/s3

---

## OUTILS ET PROCESSUS

### 🐙 Git / GitHub
**Qu'est-ce que c'est ?**
Système de contrôle de version. Tu gardais les traces de chaque changement au code, et tu peux revenir en arrière si quelque chose casse.

**En analogie simple :**
C'est comme Google Docs pour le code, mais BEAUCOUP plus puissant. Chaque changement est enregistré, tu peux voir qui a changé quoi, et tu peux revenir en arrière.

**Concepts clés :**
- **Repository** : Dossier du projet (local ou sur GitHub)
- **Commit** : Snapshot d'un état du code avec un message
- **Branch** : Version parallèle du code (ex: "feature-transcription")
- **Merge** : Fusionner deux branches

**Workflow classique :**
```bash
git clone https://github.com/xxx/nathanimage  # Télécharger le projet
git checkout -b feature/photo-upload          # Créer une branche
# ... modifier des fichiers ...
git add .                                      # Préparer les changements
git commit -m "Ajouter upload photo"           # Enregistrer
git push origin feature/photo-upload           # Envoyer à GitHub
# Puis sur GitHub : faire une "Pull Request" pour merger
```

**Site officiel** : https://github.com

---

### 🐳 Docker
**Qu'est-ce que c'est ?**
Conteneurisation. Tu empaquettes ton app dans une "boîte" avec tous ses dépendances (Python 3.11, PostgreSQL, etc.), et elle fonctionne pareil sur tout ordinateur.

**En analogie simple :**
Au lieu de dire "tu dois installer Python 3.11, puis pip install xxx, puis configurer PostgreSQL", tu dis "lance ce conteneur Docker et tout fonctionne".

**Sans Docker (problématique) :**
```
Mon ordi: "Ça marche!"
Serveur de prod: "Ça marche pas..."
Raison: version différente de Python
```

**Avec Docker (simple) :**
```
Mon ordi: "Lance ce conteneur"
Serveur de prod: "Lance ce conteneur"
Résultat: Fonctionne pareil
```

**Exemple Dockerfile (backend) :**
```dockerfile
FROM python:3.11
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0"]
```

**Avantages :**
- Reproduisibilité garantie
- Facile à déployer
- Environnement isolé

**Site officiel** : https://www.docker.com

---

### 🧪 Pytest
**Qu'est-ce que c'est ?**
Framework de test pour Python. Tu écris des petits tests pour vérifier que ton code fonctionne.

**En analogie simple :**
Au lieu de tester manuellement "est-ce que si je crée un senior ça marche ?", tu écris une fonction de test qui le fait automatiquement.

**Exemple :**
```python
def test_create_senior():
    animator = User(email="anna@xxx", id=1)
    
    senior = Senior(name="Paul", animator_id=1)
    
    assert senior.name == "Paul"
    assert senior.animator_id == 1
```

**Avantages :**
- Tests automatisés (pas besoin de tester à la main)
- Repère rapidement les bugs
- Donne confiance quand on refactor

**Site officiel** : https://pytest.org

---

### 🎨 ESLint + Prettier
**Qu'est-ce que c'est ?**
Outils pour garder le code propre et cohérent.
- **ESLint** : Repère les erreurs et mauvaises pratiques
- **Prettier** : Formatte automatiquement le code

**Analogie :**
ESLint = Grammaire du texte
Prettier = Mise en page du texte

**Exemple :**
```javascript
// Avant (ESLint + Prettier)
const  user  =   {   name:"Anna"  }

// Après
const user = { name: "Anna" }
```

**Sites officiels :**
- ESLint : https://eslint.org
- Prettier : https://prettier.io

---

### 📚 Alembic
**Qu'est-ce que c'est ?**
Migrations de base de données pour Python. Quand tu changes la structure de tes tables, Alembic crée des scripts pour migrer les données existantes.

**Analogie :**
Imagine que tu ajoutes une colonne "phone" à la table "users". Alembic fait cette modification en douceur, sans perdre les données existantes.

**Exemple :**
```bash
alembic revision --autogenerate -m "Ajouter colonne phone"
alembic upgrade head
```

**Site officiel** : https://alembic.sqlalchemy.org

---

## CONCEPTS GÉNÉRAUX

### 🔐 JWT (JSON Web Token)
**Qu'est-ce que c'est ?**
Système d'authentification. Quand un utilisateur se connecte, le backend génère un JWT qu'il stocke. À chaque requête, il envoie ce JWT pour prouver qu'il est connecté.

**En analogie simple :**
Un bracelet VIP. Tu arrives au bar, tu montres le bracelet "je suis connecté", tu peux entrer.

**Flux :**
```
1. Utilisateur envoie email + password
2. Backend valide → crée un JWT
3. Frontend stocke le JWT en localStorage
4. À chaque requête, le JWT est envoyé dans le header
5. Backend valide le JWT → savoir qui c'est
```

**Structure d'un JWT :**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjo1LCJleHAiOjE2MzIxNDM2MDB9.xxxxx

Partie 1 (Header): {"alg":"HS256","typ":"JWT"}
Partie 2 (Payload): {"user_id":5,"exp":1632143600}  ← C'est quoi, on sait qui c'est!
Partie 3 (Signature): Vérifie que le token n'a pas été modifié
```

**Sécurité :**
- ✅ Stocké en localStorage (frontend)
- ✅ Envoyé dans le header Authorization
- ✅ Expiré après 24h (tu dois te reconnecter)

---

### 🔒 Hashing de passwords
**Qu'est-ce que c'est ?**
Jamais stocker un password en clair en base de données. On le "hash" (transforme en code illisible).

**Analogie :**
C'est comme mettre le password dans un mixeur : impossible de le récupérer intègre.

**Important :**
Le hash est "unidirectionnel". Si quelqu'un accède à la DB, il ne voit pas les passwords.

**Exemple :**
```python
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"])

# Hash le password quand on crée l'utilisateur
hashed_password = pwd_context.hash("monpassword123")
# Résultat: $2b$12$abcdef...xyz (incassable)

# Quand l'utilisateur se connecte, on compare
if pwd_context.verify("monpassword123", hashed_password):
    print("Bon password!")
```

---

### 📊 API REST
**Qu'est-ce que c'est ?**
Convention pour créer des APIs. Tu utilises les verbes HTTP (GET, POST, PUT, DELETE) pour manipuler les ressources.

**Analogie :**
C'est comme le CRUD (Create, Read, Update, Delete) mais via HTTP.

**Mapping :**
```
GET    /seniors          → Récupérer tous les seniors
GET    /seniors/5        → Récupérer le senior 5
POST   /seniors          → Créer un nouveau senior
PUT    /seniors/5        → Modifier le senior 5
DELETE /seniors/5        → Supprimer le senior 5
```

**Exemple FastAPI :**
```python
@app.get("/seniors")
def list_seniors():
    return db.query(Senior).all()

@app.post("/seniors")
def create_senior(data: SeniorCreate):
    senior = Senior(**data.dict())
    db.add(senior)
    db.commit()
    return senior

@app.put("/seniors/{senior_id}")
def update_senior(senior_id: int, data: SeniorUpdate):
    senior = db.query(Senior).get(senior_id)
    for key, value in data.dict().items():
        setattr(senior, key, value)
    db.commit()
    return senior

@app.delete("/seniors/{senior_id}")
def delete_senior(senior_id: int):
    db.query(Senior).filter(Senior.id == senior_id).delete()
    db.commit()
    return {"ok": True}
```

---

### 📡 HTTP Status Codes
**Qu'est-ce que c'est ?**
Codes que le serveur retourne pour dire "ça a marché" ou "erreur".

**Codes principaux :**
```
200 OK                      → Succès
201 Created                 → Créé avec succès
400 Bad Request             → Données invalides (frontend error)
401 Unauthorized            → Pas connecté
403 Forbidden               → Pas les permissions
404 Not Found               → Ressource n'existe pas
500 Internal Server Error   → Erreur backend
```

**Exemple :**
```python
@app.get("/seniors/{senior_id}")
def get_senior(senior_id: int):
    senior = db.query(Senior).get(senior_id)
    if not senior:
        return {"error": "Senior not found"}, 404  # 404 Not Found
    return senior  # 200 OK implicite
```

---

### 🔄 CORS (Cross-Origin Resource Sharing)
**Qu'est-ce que c'est ?**
Règle de sécurité qui dit "quels domaines peuvent accéder à mon API".

**Pourquoi ?**
Si ton frontend est sur `app.nathanimage.com` et l'API sur `api.nathanimage.com`, le navigateur refuse d'appeler l'API par défaut (sécurité).

**Configuration FastAPI :**
```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000", "https://app.nathanimage.com"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

---

## 🎓 Résumé : Points clés à retenir

| Technologie | Rôle | Pourquoi |
|---|---|---|
| **React** | Créer l'interface | Simple, populaire, composants réutilisables |
| **TypeScript** | Ajouter des types | Attrape les erreurs avant runtime |
| **Redux** | Gestion d'état | Données centralisées, facile d'accès partout |
| **FastAPI** | Créer l'API backend | Rapide, simple, auto-documentation |
| **PostgreSQL** | Stocker les données | Fiable, puissant, gratuit |
| **JWT** | Authentification | Sécurisé, stateless |
| **AWS S3** | Stocker photos/audio | Scalable, pas cher, rapide |
| **Whisper** | Transcription audio | Très précis, 50+ langues |
| **Claude** | Génération IA | Qualité texte excellente |
| **Docker** | Déploiement | Pareil partout, facile à scaler |

---

## 📚 Ressources pour apprendre

**Par ordre de priorité pour NathAnimÂge :**

1. **React + TypeScript** : https://react.dev
2. **FastAPI** : https://fastapi.tiangolo.com
3. **Redux Toolkit** : https://redux-toolkit.js.org
4. **SQLAlchemy** : https://www.sqlalchemy.org
5. **PostgreSQL** : https://www.postgresql.org/docs
6. **JWT** : https://jwt.io
7. **AWS S3** : https://docs.aws.amazon.com/s3

---

## 🆘 En cas de doute

Utilise ChatGPT ou Claude pour :
- "Comment utiliser Whisper API avec Python ?"
- "Comment faire un upload de fichier avec Axios ?"
- "Quelle est la meilleure pratique pour structurer Redux ?"

Ils répondront mieux que tu peux l'imaginer.

**Bon courage !** 🚀
