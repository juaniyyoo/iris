# Documentation du POC UX/UI

## Objectif

Le POC doit permettre aux futures utilisatrices de manipuler une representation realiste de NathAnimAge avant d'engager le developpement professionnel.

Il valide l'experience, pas la technique. Toutes les donnees sont fictives et toutes les actions sont simulees localement.

## Documents

1. [Cahier de validation UX/UI](01-CAHIER-VALIDATION-UX-UI.md) : perimetre, ecrans, parcours et criteres d'acceptation.
2. [Prompt de generation du POC](02-PROMPT-GENERATION-POC.md) : texte pret a donner a un outil de generation.
3. [Passage a la version professionnelle](03-PASSAGE-VERSION-PRO.md) : decisions a conserver et methode de transition.

## Definition de "sans module externe"

Pour ce POC :

- aucune installation de paquet ;
- aucun framework frontend ;
- aucun backend ;
- aucune base de donnees ;
- aucun appel a une API ;
- aucune cle ou variable d'environnement ;
- aucune authentification reelle ;
- aucun envoi de photo ou d'audio vers un serveur.

Le navigateur suffit pour consulter le resultat genere.

## Ce que le POC ne prouve pas

Le POC ne valide ni la faisabilite de l'IA, ni la securite, ni la conformite RGPD, ni les performances, ni le cout des services. Ces sujets appartiennent a la documentation de l'application complete.
