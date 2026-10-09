# NathAnimAge - Du POC a l'application professionnelle v4

Ce depot contient uniquement la documentation necessaire pour valider l'experience utilisateur, puis faire generer l'application complete.

## Les deux etapes

### 1. Valider le POC UX/UI

Le POC sert a tester les ecrans, les textes et les parcours avec les animatrices et les familles. Il ne doit contenir ni backend, ni base de donnees, ni authentification reelle, ni service externe.

1. Lire le [cahier de validation UX/UI](documentation/poc/01-CAHIER-VALIDATION-UX-UI.md).
2. Ajuster les ecrans et les criteres avec les personnes qui testeront le POC.
3. Utiliser le [prompt de generation du POC](documentation/poc/02-PROMPT-GENERATION-POC.md) dans l'outil de generation choisi.
4. Faire tester le resultat et noter les decisions dans la grille de validation.
5. Regenerer le POC jusqu'a validation des parcours principaux.

Le POC est volontairement jetable. Il sert a prendre des decisions de produit, pas a devenir progressivement l'application de production.

### 2. Generer la version professionnelle

Une fois l'UX/UI validee :

1. Consolider les decisions prises pendant les tests.
2. Lire la [documentation de l'application complete](documentation/application-complete/README.md).
3. Suivre le [guide de passage a la version professionnelle](documentation/poc/03-PASSAGE-VERSION-PRO.md).
4. Adapter puis utiliser le [prompt de generation de l'application complete](documentation/application-complete/02-PROMPT-BOILERPLATE.md).
5. Construire et verifier les fonctionnalites par lots, en commencant par le parcours animatrice.

## Arborescence

```text
documentation/
|-- application-complete/  Reference fonctionnelle et technique de la vraie application
|-- poc/                    Cadrage, generation et validation du prototype UX/UI
`-- README.md               Index des documents
```

## Regle simple

- Une question sur l'apparence, les libelles ou la navigation se traite dans le POC.
- Une question sur les donnees, la securite, l'IA, le stockage ou le deploiement se traite dans l'application complete.
- Une decision UX validee dans le POC doit etre reportee explicitement dans le cahier de la version professionnelle avant sa generation.
