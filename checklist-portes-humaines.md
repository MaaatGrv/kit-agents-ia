# Les trois portes humaines

L'agent prépare, propose, prouve. **Toi, tu ouvres la porte.** Il n'en passe aucune seul.

---

## Porte 1 : décisions produit, avant le code

**Qui décide :** toi (le product builder). Pas l'agent.

- [ ] L'agent a lu le code concerné et dit ce qui **existe déjà** et ce qui **manque**.
- [ ] Il m'a posé ses questions produit (comportement, cas limites, périmètre, texte affiché), et j'ai répondu.
- [ ] Le périmètre est écrit dans le ticket : ce qu'on fait, et ce qu'on **ne** fait **pas**.
- [ ] Je sais à quoi ressemble « fini » : une phrase que je pourrai vérifier moi-même.
- [ ] Si ça touche à l'argent, aux droits ou aux données perso, je l'ai signalé.

> **Piège réel :** 4 défauts que les tests ne voyaient pas, trouvés en QA navigateur : un titre de notification tronqué à 390 px, un compteur faux côté admin, un flash à l'ouverture d'une page, une modale qui ne prévenait pas d'une conséquence. Ce que « fini » veut dire, ce n'est pas aux tests de le décider.

---

## Porte 2 : QA, avant le merge

**Qui décide :** toi, après avoir testé. Une CI verte n'est pas un « oui ».

- [ ] Chaque « c'est bon » de la PR pointe vers une **preuve** : commande, sortie, lien, capture.
- [ ] La PR a une section **« NON couvert »** et une section **« Non vérifié »**. Je les ai lues.
- [ ] J'ai déroulé la fiche QA moi-même, dans le navigateur, sur mobile **et** sur ordinateur.
- [ ] J'ai testé le chemin qui doit **échouer** (mauvaise saisie, mauvais compte, double clic), pas seulement le chemin heureux.
- [ ] Les droits sont testés avec de **vrais comptes de test**, un par rôle : l'utilisateur A ne voit pas les données de B.
- [ ] Une fonction de base de données a été exécutée sur une vraie base, pas seulement dans des tests qui la simulent.
- [ ] Le code cité dans la PR existe encore dans la version finale de la branche.

> **Piège réel :** 2 129 tests verts, CI verte, 3 revues, et un appel serveur en erreur 500 dans 100 % des cas. Les tests simulaient la base : la fonction n'avait jamais tourné.
>
> **Piège réel :** une PR annonçait « gate qualité OK » sur du code déjà supprimé.

---

## Porte 3 : mise en prod

**Qui décide :** toi, et personne d'autre. L'agent prépare la liste, tu appuies sur le bouton.

- [ ] Les **migrations** de base sont listées, appliquées **avant** le code, et leur effet vérifié (la table, la colonne, la fonction existent vraiment).
- [ ] Je sais comment revenir en arrière si ça casse, et combien de temps ça prend.
- [ ] Après le déploiement, je vérifie que **la bonne version** est en ligne, pas juste que le site répond.
- [ ] Je refais le parcours principal en prod, avec un compte de test.
- [ ] Je surveille les erreurs pendant l'heure qui suit.

> **Piège réel :** un lot parti en prod sans ses migrations, modération cassée environ 2 h. Le code se déploie tout seul, le schéma de base non.

---

## À chaque porte

**Sécurité**
- [ ] Aucun secret (clé d'API, mot de passe, token) dans la conversation, le code, les commits ou la PR.
- [ ] Les fichiers de secrets sont hors de portée de l'agent (ignorés par git, jamais collés dans le chat).
- [ ] L'agent n'a que les accès dont il a besoin. Pas d'accès en écriture à la prod pour un agent qui code.

**RGPD**
- [ ] Aucune vraie donnée personnelle dans les prompts : pas de vrai nom, e-mail, téléphone, adresse. Des données inventées.
- [ ] Les logs et captures d'écran collés à l'agent sont anonymisés.

**Coût**
- [ ] Je connais le prix d'une session : tokens, CI, déploiements. Je le regarde une fois par semaine.
- [ ] Un agent qui tourne en boucle sans avancer, je l'arrête.
- [ ] Je regroupe les petits tickets voisins plutôt que de lancer un agent neuf pour chacun.
