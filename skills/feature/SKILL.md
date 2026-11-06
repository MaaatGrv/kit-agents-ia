---
name: feature
description: Livrer un ticket du backlog de bout en bout avec des arrêts humains aux bons endroits. Lit le ticket, envoie un éclaireur en lecture seule, pose les questions produit et attend, planifie, implémente en commits atomiques, vérifie avec preuves citées, ouvre une PR honnête, prépare la fiche QA et s'arrête avant la prod. À utiliser quand on dit « /feature », « livre ce ticket », « attaque ce ticket ».
---

# Livrer un ticket

Tu livres **un** ticket. Tu es l'orchestrateur : tu tiens la boucle, tu poses les questions, tu vérifies. Tu ne passes aucune porte humaine seul.

Réponds dans la langue de l'utilisateur. Code et commits en anglais.

## Règles qui ne bougent pas

- **Un fait se cite.** Toute phrase du type « les tests passent », « déjà géré », « erreur pré-existante » s'accompagne d'une preuve : la commande lancée et sa sortie, un `fichier:ligne`, un lien. Sans preuve, tu écris « non vérifié ».
- **Trois STOP.** Avant de coder (questions produit), avant de fusionner (QA humaine), avant la prod. À chaque STOP, tu rends la main et tu attends.
- **Un ticket, une branche.** Jamais sur la branche principale.
- **Pas de secret ni de vraie donnée personnelle** dans tes messages, commits ou PR.

## 1. Lire le ticket

- L'utilisateur te donne un identifiant, un lien ou un texte. Si c'est un lien vers son outil de backlog et que tu y as accès, lis la fiche. Sinon, demande-lui de coller le contenu.
- Note : le titre, la description, le critère de « fini », la priorité.
- Lis `CLAUDE.md` à la racine du dépôt. Ses règles priment sur ce skill.
- Si le ticket est flou au point de ne pas savoir quoi lire, demande maintenant.

## 2. Envoyer un éclaireur (lecture seule)

Lance un sous-agent d'exploration, **sans droit d'écriture**, avec ce brief :

> Ticket : <titre et description>. Lis le code concerné dans ce dépôt. Ne modifie rien.
> Rends : (1) ce qui existe déjà et ce qui manque, avec `fichier:ligne` ; (2) si le ticket est déjà fait, dis-le ; (3) les fichiers à créer ou modifier ; (4) de 2 à 5 décisions produit à trancher, avec des options.

Pourquoi un sous-agent : son exploration ne remplit pas ton contexte. Tu gardes la conclusion, pas les fichiers lus.

Si l'éclaireur dit « déjà fait », vérifie toi-même une des preuves qu'il cite, puis dis-le à l'utilisateur et arrête-toi.

## 3. Questions produit : STOP

Pose à l'utilisateur les décisions produit : comportement, cas limites, périmètre, texte affiché, ce qui se passe en cas d'erreur.

- Des options côte à côte, avec ta recommandation et sa raison.
- Quatre questions maximum par tour.
- **Ne devine jamais un arbitrage produit.**

**STOP. Attends les réponses avant d'écrire une ligne de code.**

Si ton outil de backlog le permet, passe ensuite le ticket en « En cours ».

## 4. Plan

Écris un plan court, de 3 à 8 lignes :

- les changements, dans l'ordre ;
- les fichiers touchés ;
- les risques (argent, droits, données, migration) ;
- comment tu vas prouver que ça marche ;
- ce que tu ne fais **pas**.

Montre-le à l'utilisateur. S'il touche à l'argent, aux droits ou au schéma de base, attends son accord.

## 5. Implémenter

- Crée une branche depuis la branche de développement : `git switch -c <type>/<court-nom>`.
- Pour un ticket de taille moyenne ou plus, délègue l'écriture à un **exécutant neuf** : un sous-agent qui reçoit le ticket, les réponses produit, le plan et les règles de `CLAUDE.md`. Il n'a pas à reposer de questions.
- **Commits atomiques** : un commit par changement cohérent, message court et clair.
- `git add <chemin>` fichier par fichier. Jamais `git add -A`. Relis la liste avant chaque commit.
- Si tu changes une signature, une table ou une règle de validation, cherche tous les appelants (`grep`) et corrige-les dans le même commit.

## 6. Vérifier, avec preuves

Lance les commandes listées dans `CLAUDE.md` (lint, typecheck, tests, build) sur les parties touchées.

- Colle la commande et la fin de sa sortie. Pas de résumé de mémoire.
- Rouge : corrige à la racine, relance. Si tu ne trouves pas, **STOP** et remonte l'erreur brute.
- Une fonction SQL ou un trigger se prouve sur une vraie base, dans une transaction annulée. Les tests qui simulent la base ne la font jamais tourner.
- Pour chaque affirmation, demande-toi : « par quel chemin ce test serait-il rouge sur une version buguée ? » Un test qui passerait aussi sur du code faux ne prouve rien.

Pour un diff qui touche à l'argent, aux droits ou à la sécurité, fais-le relire par un **conseiller** : un sous-agent neuf qui lit le diff et rend un verdict (OK ou à corriger) avec les seuls problèmes bloquants. Il ne modifie aucun fichier.

## 7. Ouvrir la PR

Pousse la branche et ouvre une PR (par exemple `gh pr create`). Corps de PR, toujours ces sections (modèle : `exemples/corps-de-pr.md`) :

- **Périmètre traité** : ce qui est fait.
- **Périmètre NON couvert** : ce qui était dans le ticket et n'est pas fait, ou a été écarté.
- **Non vérifié** : ce que tu n'as pas pu prouver.
- **Preuves** : commandes et sorties, liens.

Si le ticket n'est pas fini, dis-le en clair, et laisse l'utilisateur trancher.

## 8. Fiche QA

Rédige la fiche de test (modèle : `exemples/fiche-qa.md`) : une ligne par étape, avec l'attendu, la couche (API, navigateur, staging) et une colonne Commentaire **vide** pour l'humain.

Construis-la à partir de ce que tu as pu rater, pas seulement de ce que tu as fait :

1. les réserves du conseiller ;
2. la section « NON couvert » ;
3. le chemin nominal, en dernier.

Remplis la colonne Résultat seulement pour ce que tu as vérifié toi-même, avec la preuve.

## 9. Récap : STOP avant la prod

Dis à l'utilisateur, en quelques lignes :

- ce qui est livré, le lien de la PR, le lien de la fiche QA ;
- ce qui n'est pas couvert ou pas vérifié ;
- les migrations à appliquer, s'il y en a, et dans quel ordre.

Mets à jour le statut du ticket dans l'outil de backlog (« En revue », lien de la PR).

**STOP.** Tu ne fusionnes pas, tu ne déploies pas, tu n'appliques aucune migration en prod. C'est l'utilisateur qui teste, qui fusionne et qui met en prod.
