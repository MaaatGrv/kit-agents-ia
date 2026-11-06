# Modèle de fiche QA

Une fiche par ticket. L'agent la prépare, l'humain la déroule et remplit la colonne Commentaire.

**Couches :**
- **API** : vérifiable par l'agent, en appelant le serveur.
- **Navigateur** : à faire par un humain, à l'écran, sur mobile et ordinateur.
- **Staging** : sur l'environnement de préprod déployé, avec les comptes de test.

**Résultat :** ✅ conforme, ❌ écart (écrire attendu contre obtenu), ⚠️ partiel, vide si pas encore testé.

---

## <Identifiant du ticket> : <titre court>

**Environnement :** <lien de préprod>, PR <numéro>, version <identifiant du commit>
**Comptes de test :** <rôle A> : <compte de test A> · <rôle B> : <compte de test B>
**État initial :** <données à préparer avant de commencer>

| # | Étape | Attendu | Couche | Résultat | Commentaire |
|---|---|---|---|---|---|
| 1 | <Action précise : où cliquer, quoi saisir> | <Ce qui doit s'afficher ou se passer> | Navigateur | | |
| 2 | <Action> | <Attendu> | API | ✅ <preuve courte de l'agent> | |
| 3 | <Le même parcours avec le mauvais compte> | <Accès refusé, rien ne fuit> | Staging | | |
| 4 | <Saisie invalide ou double clic> | <Message clair, pas de doublon> | Navigateur | | |
| 5 | <Écran à 390 px de large> | <Rien de tronqué, rien qui déborde> | Navigateur | | |

**Reset :** <comment remettre l'état initial pour rejouer la fiche>

---

## Exemple rempli

## TICKET-142 : Export CSV des commandes

**Environnement :** préprod, PR 87
**Comptes de test :** admin : compte de test admin · client : compte de test client
**État initial :** 87 commandes de test, dont 3 annulées.

| # | Étape | Attendu | Couche | Résultat | Commentaire |
|---|---|---|---|---|---|
| 1 | Admin > Commandes, cliquer « Exporter » | Un fichier CSV se télécharge | Navigateur | | |
| 2 | Appeler la route d'export avec le compte admin | 87 lignes, 4 colonnes | API | ✅ 87 lignes, colonnes conformes | |
| 3 | Appeler la route d'export avec le compte client | Refus (403), aucune donnée | API | ✅ 403 | |
| 4 | Filtrer sur « annulées », puis exporter | 3 lignes seulement | Navigateur | | |
| 5 | Ouvrir le fichier dans un tableur | Accents corrects, montants lisibles | Navigateur | | |
| 6 | Page Commandes sur mobile, 390 px | Le bouton est visible et cliquable | Navigateur | | |

## Comment écrire une bonne étape

- **Précise.** « Cliquer sur Exporter en haut à droite », pas « tester l'export ».
- **Qui peut échouer.** Pose-toi la question : cette étape serait-elle rouge sur une version buguée ? Si non, elle ne teste rien.
- **Avec le mauvais compte.** Au moins une étape par ticket vérifie que quelqu'un qui n'a pas le droit ne voit rien.
- **Colonne Commentaire vide.** C'est la place de l'humain. L'agent ne la remplit pas.
