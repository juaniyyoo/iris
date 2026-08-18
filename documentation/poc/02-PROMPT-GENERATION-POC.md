# Prompt de generation du POC

## Utilisation

1. Lire et adapter le cahier de validation avant toute generation.
2. Copier le prompt ci-dessous dans l'outil de generation choisi.
3. Joindre le [cahier de validation UX/UI](01-CAHIER-VALIDATION-UX-UI.md) si l'outil accepte des fichiers.
4. Faire executer le resultat localement dans un navigateur.
5. Tester, noter les retours, modifier le cahier puis regenerer si necessaire.

## Prompt a copier

```text
Tu dois generer un POC UX/UI local et jetable pour l'application "NathAnimAge".

OBJECTIF
Permettre a des animatrices et a des familles de valider les ecrans, les libelles et les parcours avant le developpement de l'application professionnelle. Le POC ne doit pas chercher a valider l'architecture technique.

CONTRAINTE ABSOLUE
N'utilise aucun module, paquet, framework, CDN, service externe, backend, base de donnees ou API. Le resultat doit fonctionner localement avec les fonctions natives d'un navigateur moderne, sans installation et sans connexion Internet.

PUBLICS
- Animatrice : documente rapidement une seance a domicile.
- Famille : consulte un journal de vie prive et simple.

ECRANS ATTENDUS
1. Accueil animatrice avec seniors et seances recentes.
2. Choix du senior.
3. Seance en cours avec photo, audio et notes simules.
4. Recapitulatif de fin de seance.
5. Compte rendu fictif, modifiable avant partage.
6. Confirmation de partage et rappel de ce que la famille verra.
7. Journal famille chronologique.

PARCOURS PRINCIPAL
L'animatrice choisit Marie Dupont, demarre une seance, ajoute une photo fictive, un audio fictif et une note, termine la seance, attend une courte generation simulee, modifie le compte rendu puis le partage. Le resultat apparait ensuite dans la vue famille.

DONNEES DE DEMONSTRATION
- Animatrice : Nathalie Martin.
- Seniors : Marie Dupont, Andre Robert et Jeanne Leroy.
- Seance : atelier cuisine autour d'une tarte aux pommes.
- Note initiale : "Marie a choisi les pommes et raconte une recette de son enfance."
- Toutes les donnees sont fictives et doivent etre presentees comme telles.

EXPERIENCE ATTENDUE
- Interface en francais, responsive, accessible et utilisable au tactile.
- Style chaleureux mais professionnel, adapte a un outil de travail et non a une page marketing.
- Navigation claire entre l'espace animatrice et l'apercu famille.
- Un seul appel a l'action principal par etape.
- Etats vide, en cours, termine et partage clairement visibles.
- Confirmations avant fin de seance et avant partage.
- Aucun jargon technique visible.
- Aucun texte expliquant comment utiliser l'interface dans l'interface elle-meme.

SIMULATIONS AUTORISEES
- Donnees statiques locales.
- Minuteur visuel.
- Ajout ou suppression de medias fictifs.
- Lecture audio fictive.
- Court etat de chargement pour la generation.
- Conservation temporaire des choix dans le navigateur.

INTERDICTIONS
- Ne demande aucune cle API.
- N'utilise aucune vraie donnee personnelle.
- Ne declenche pas la camera ou le microphone.
- Ne simule pas une sauvegarde distante reelle.
- N'ajoute pas d'authentification, de paiement ou d'administration.
- Ne presente pas ce POC comme une base de production.

LIVRABLE
Fournis le minimum de fichiers statiques clairement nommes, les instructions tres courtes pour ouvrir le POC dans un navigateur, et une liste des parcours effectivement simulables. Ne fournis aucune architecture backend ou configuration de production.

Avant de terminer, verifie chaque ecran sur un format mobile et un format ordinateur, puis confirme que le parcours complet peut etre realise sans erreur et sans connexion reseau.
```

## Demandes de correction utiles

Apres un test, ne demandez pas une regeneration vague. Decrivez le probleme observe, la decision prise et le critere de reussite.

Exemple :

```text
Sur l'ecran de fin de seance, deux testeuses n'ont pas compris que le compte rendu serait encore modifiable. Remplace le libelle principal par "Terminer et relire", ajoute un etat intermediaire de relecture, et conserve le partage dans une etape separee.
```
