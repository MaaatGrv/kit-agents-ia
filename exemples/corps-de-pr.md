# Modèle de corps de PR honnête

Une bonne PR d'agent ne dit pas seulement ce qui marche. Elle dit ce qui manque et ce qui n'est pas prouvé. C'est ce qui te permet de décider vite.

Copie le bloc ci-dessous. Remplace les `<…>`.

---

```markdown
## <Titre court du ticket> (<identifiant du ticket>)

Lien du ticket : <lien vers ton outil de backlog>

### Périmètre traité
- <Changement 1, du point de vue de l'utilisateur>
- <Changement 2>
- <Changement technique notable, s'il y en a un : migration, nouvelle route>

### Périmètre NON couvert
- <Ce qui était dans le ticket et n'est pas fait>, parce que <raison>.
- <Ce qui a été écarté volontairement>, décidé par <qui> le <date>.

### Non vérifié
- <Ce que l'agent n'a pas pu prouver> : <pourquoi> (pas d'accès, pas de compte de test, à tester sur mobile).

### Preuves
- Lint, typecheck, tests : `<commande>` → `<dernière ligne de sortie>`
- Fonction de base testée sur une vraie base : `<commande>` → `<résultat>`
- Capture ou lien de préprod : <lien>

### Migrations
- <Aucune> / <nom du fichier>, à appliquer **avant** le merge.

### Fiche QA
<lien vers la fiche>
```

---

## Exemple rempli

```markdown
## Export CSV des commandes (TICKET-142)

### Périmètre traité
- Bouton « Exporter » sur la page Commandes, côté admin.
- Export des commandes filtrées, en CSV, colonnes : date, client, montant, statut.

### Périmètre NON couvert
- L'export des commandes **remboursées**. Le ticket le demande, mais la table
  des remboursements n'a pas de lien direct vers la commande d'origine.
  Il faut une migration, et elle touche au calcul des montants.

### Non vérifié
- Un export de plus de 1 000 lignes : la base de préprod n'en a que 87.
  La requête est paginée (`orders-export.ts:42`) mais je ne l'ai pas vue tourner sur un gros volume.

### Preuves
- `npm run lint && npm run test -- orders` → `Tests: 14 passed, 14 total`
- Préprod : <lien vers la page>, export téléchargé et ouvert, 87 lignes.
```

> Ce ticket n'est donc pas fini. C'est <toi> qui tranches. Option A : je livre l'export sans les remboursements maintenant et j'ouvre un ticket pour la migration. Option B : j'attends ton feu vert pour faire la migration dans cette PR. Je recommande A : la migration touche au calcul des montants et mérite sa propre QA.

C'est le comportement attendu d'un agent. Il ne cache pas le trou sous un « done ». Il le montre, il donne les options, et il te laisse décider.

## Les signaux d'alerte

Si une PR d'agent contient une de ces phrases sans preuve à côté, demande la preuve :

- « Tous les tests passent. »
- « Gate qualité OK. »
- « Erreur pré-existante, sans rapport. »
- « Déjà géré ailleurs. »
- « Aucun impact sur le reste. »
