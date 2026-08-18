# Passer du POC a la version professionnelle

## Principe

Le POC et l'application professionnelle sont deux livrables distincts.

- Le POC valide ce que les utilisateurs voient et font.
- La version professionnelle garantit que ces actions fonctionnent avec de vraies donnees, de vraies permissions et des services securises.

Il est preferable de reconstruire la version professionnelle selon l'architecture cible plutot que d'etendre le code jetable du POC.

## 1. Fermer la phase POC

Avant la generation de la version professionnelle :

1. Completer la grille du cahier de validation.
2. Lister les ecrans retenus et ceux abandonnes.
3. Figer les libelles principaux.
4. Documenter le parcours animatrice valide.
5. Documenter ce que la famille peut voir.
6. Lister les points encore incertains sans les masquer.
7. Conserver des captures des ecrans valides comme reference visuelle.

## 2. Transformer les simulations en besoins reels

| Dans le POC | Dans la version professionnelle |
|---|---|
| Senior fictif | Senior en base, rattache a l'animatrice autorisee |
| Connexion simulee | Authentification et gestion des roles |
| Photo fictive | Permission, compression, envoi et stockage securise |
| Audio fictif | Permission, enregistrement, envoi et transcription |
| Note locale | Sauvegarde fiable et recuperation apres interruption |
| Generation simulee | Traitement asynchrone, IA, erreurs et nouvelle tentative |
| Partage simule | Consentement, droits d'acces et journal d'audit |
| Journal famille | API filtree selon les permissions et medias proteges |
| Donnees temporaires | Base de donnees, sauvegardes et suppression RGPD |

## 3. Ordre de realisation recommande

1. **Socle** : environnements, base de donnees, journalisation et conventions de securite.
2. **Identites** : authentification, roles animatrice/famille et autorisations.
3. **Seniors** : creation, consultation, modification, suppression et consentements.
4. **Seances** : cycle brouillon, en cours, terminee et partagee.
5. **Notes et medias** : sauvegarde, photo, audio et reprise en cas d'echec.
6. **Compte rendu** : transcription, generation, relecture et historique des modifications.
7. **Partage famille** : invitations, permissions et journal prive.
8. **Exploitation** : tests, supervision, sauvegardes, RGPD et deploiement.
9. **Offre payante** : limite gratuite et facturation, apres validation de l'usage principal.

Chaque lot doit reprendre les ecrans valides du POC et ajouter les etats techniques necessaires : chargement, erreur, absence de reseau, reprise et refus de permission.

## 4. Elements a fournir a l'outil de generation

- toute la documentation du dossier `application-complete` ;
- le cahier de validation POC complete ;
- les captures d'ecran retenues ;
- la liste des decisions UX definitives ;
- la liste des exigences RGPD et de securite ;
- les contraintes d'hebergement et de budget ;
- le lot precis a generer, avec ses criteres d'acceptation.

Ne demandez pas de generer toute l'application en une seule reponse. Utilisez le prompt complet comme contexte, puis demandez un lot testable a la fois.

## 5. Adaptation du prompt de l'application complete

Le prompt existant se trouve dans [02-PROMPT-BOILERPLATE.md](../application-complete/02-PROMPT-BOILERPLATE.md). Avant de l'utiliser :

1. Remplacer les suppositions UX par les decisions validees.
2. Verifier que la stack technique est toujours souhaitee.
3. Retirer les fonctionnalites non prioritaires.
4. Ajouter les criteres d'acceptation du premier lot.
5. Exiger des tests automatises pour les regles metier et les autorisations.
6. Exiger une validation humaine avant toute mise en production.

## 6. Portes de validation professionnelles

La version professionnelle n'est pas prete au deploiement tant que les points suivants ne sont pas verifies :

- aucune donnee de sante ou donnee personnelle n'est exposee sans autorisation ;
- les roles et permissions sont testes cote serveur ;
- le consentement photo et audio est tracable ;
- l'utilisateur peut corriger un compte rendu avant partage ;
- la suppression et l'export des donnees sont prevus ;
- les secrets ne sont jamais presents dans le frontend ;
- les echecs d'IA, de stockage et de reseau ont un comportement explicite ;
- les sauvegardes et la restauration sont testees ;
- les couts des services externes sont mesurables ;
- les parcours valides dans le POC restent reconnaissables.
