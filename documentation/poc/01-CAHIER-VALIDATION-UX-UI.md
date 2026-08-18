# Cahier de validation UX/UI du POC

## 1. But du test

Verifier qu'une animatrice peut documenter une seance en quelques minutes et qu'un membre de la famille comprend facilement le journal de vie partage.

Le test doit repondre a trois questions :

1. L'utilisatrice sait-elle immediatement quoi faire ?
2. Peut-elle terminer le parcours sans aide ?
3. Les informations affichees sont-elles utiles, rassurantes et comprehensibles ?

## 2. Publics a representer

### Animatrice

Elle intervient a domicile, parfois depuis un telephone. Elle doit pouvoir selectionner une personne, lancer une seance, ajouter des traces, relire un compte rendu et choisir de le partager.

### Famille

Elle consulte un journal prive depuis un telephone ou un ordinateur. Elle cherche surtout des nouvelles recentes, des photos et une lecture simple de la seance.

## 3. Perimetre fonctionnel du POC

Le POC doit simuler les ecrans suivants :

1. **Accueil animatrice** : prochaine action visible, liste courte de seniors et seances recentes.
2. **Choix du senior** : selection d'une fiche avant de commencer une seance.
3. **Seance en cours** : chronometre simule, ajout de photo, ajout d'audio et zone de notes.
4. **Recapitulatif** : traces ajoutees, possibilite de revenir corriger ou de terminer.
5. **Compte rendu genere** : texte fictif modifiable, choix des photos et action de partage.
6. **Confirmation de partage** : indication claire de ce que la famille pourra voir.
7. **Journal famille** : fil chronologique avec compte rendu, photos et instant audio simule.

Une navigation permet de basculer explicitement entre la vue animatrice et la vue famille pendant les tests.

## 4. Parcours principal a tester

### Parcours animatrice

1. Arriver sur l'accueil.
2. Demarrer une nouvelle seance.
3. Choisir Marie Dupont dans des donnees fictives.
4. Ajouter une photo simulee.
5. Ajouter un enregistrement audio simule.
6. Saisir une note courte.
7. Terminer la seance.
8. Lancer la generation simulee du compte rendu.
9. Relire et modifier une phrase.
10. Partager le compte rendu avec la famille.

### Parcours famille

1. Ouvrir le journal de Marie Dupont.
2. Identifier la seance la plus recente.
3. Lire le resume.
4. Consulter les medias associes.
5. Comprendre la date, l'activite et l'identite de l'animatrice.

## 5. Donnees fictives minimales

- Animatrice : Nathalie Martin.
- Senior principal : Marie Dupont, 84 ans.
- Autres seniors : Andre Robert et Jeanne Leroy.
- Seance du jour : atelier cuisine, preparation d'une tarte aux pommes.
- Note : "Marie a choisi les pommes et raconte une recette de son enfance."
- Compte rendu fictif : texte chaleureux, factuel et court, clairement presente comme modifiable avant partage.
- Medias : trois images de demonstration locales ou zones d'illustration et un audio simule.

Aucune vraie donnee personnelle ne doit etre utilisee pendant les tests.

## 6. Principes d'interface

- Le parcours principal reste visible et prioritaire.
- Les actions utilisent des verbes precis : "Demarrer une seance", "Ajouter une photo", "Terminer et relire", "Partager avec la famille".
- Les actions irreversibles demandent une confirmation.
- La cible tactile des commandes principales est confortable sur mobile.
- Les etats vide, en cours, termine et partage sont visuellement distincts.
- Le texte reste lisible sans jargon technique.
- Les informations sensibles ne sont jamais presentees comme publiques.
- L'interface fonctionne sur un petit ecran mobile et sur un ordinateur.

## 7. Interactions a simuler

- changement de vue par navigation ;
- selection d'un senior ;
- ajout et suppression d'un media fictif ;
- demarrage et arret visuel d'un audio fictif ;
- saisie et conservation locale des notes pendant la session du navigateur ;
- chargement court simulant la generation du compte rendu ;
- modification du compte rendu ;
- confirmation de partage ;
- affichage du resultat dans le journal famille.

Les interactions camera, microphone, IA et partage serveur ne doivent pas etre reelles.

## 8. Criteres d'acceptation

Le POC est valide lorsque :

- au moins trois personnes representatives terminent le parcours animatrice sans explication et sans blocage ;
- le bouton principal de chaque ecran est identifie rapidement ;
- les testeurs comprennent que le compte rendu doit etre relu avant partage ;
- les testeurs savent quelles informations deviennent visibles par la famille ;
- la famille identifie la seance la plus recente et comprend son contenu ;
- aucun texte ne laisse croire que des donnees ont ete reellement sauvegardees ou envoyees ;
- les parcours sont utilisables sur mobile et sur ordinateur ;
- les remarques bloquantes ont ete corrigees ou acceptees explicitement.

## 9. Grille de test

| Point observe | Resultat | Commentaire / decision |
|---|---|---|
| Demarrage d'une seance compris | A valider | |
| Selection du senior comprise | A valider | |
| Ajout photo/audio compris | A valider | |
| Fin de seance comprise | A valider | |
| Relecture avant partage comprise | A valider | |
| Visibilite famille comprise | A valider | |
| Journal famille facile a parcourir | A valider | |
| Utilisation mobile confortable | A valider | |
| Libelles definitifs approuves | A valider | |

## 10. Hors perimetre

- creation de compte et connexion reelles ;
- permissions camera et microphone reelles ;
- transcription audio ;
- generation par intelligence artificielle ;
- stockage et compression des fichiers ;
- paiement et limitation a cinq seniors ;
- notifications ;
- administration ;
- securite, sauvegarde et deploiement.
