# Kit agents IA : construire un vrai produit avec des agents

Le modèle, tout le monde l'a. Ce qui compte, c'est ce que tu construis autour : le **harness**.

Ce kit, c'est ce harness, en version de poche. Des fichiers à copier dans ton projet pour qu'un agent de code (Claude Code ou un autre) travaille comme un collègue sérieux : il lit avant d'écrire, il te pose les questions produit, il prouve ce qu'il affirme, et il s'arrête avant de mettre en prod.

Il vient d'un retour d'expérience réel : un an à construire une plateforme qui met en relation des marques et des créateurs de contenu, payés à la performance, avec des agents IA qui écrivent l'essentiel du code. Les pièges racontés dans ces fichiers sont arrivés pour de vrai.

## Pour qui

- **Tu ne codes pas, ou peu.** Tu veux piloter un agent sans te faire balader. Commence par la [checklist des portes humaines](checklist-portes-humaines.md) : c'est elle qui te protège.
- **Tu codes déjà.** Tu veux passer de « je discute avec un chatbot » à « j'ai une méthode ». Prends le [modèle de CLAUDE.md](CLAUDE.md.template) et le [skill d'exemple](skills/feature/SKILL.md).

## La méthode en 4 règles

1. **Le contexte s'écrit** : la spec vit dans le repo (CLAUDE.md), le ticket dans l'outil de backlog.
2. **Un agent, un rôle** : l'orchestrateur ne code pas, un éclaireur lit, un exécutant neuf par ticket, un conseiller relit sans jamais écrire.
3. **Un fait se cite, il ne se rappelle pas** : chaque affirmation d'un agent (« tests verts », « gate OK ») pointe vers une preuve (commande, sortie, lien).
4. **Trois portes humaines** : décisions produit avant le code, QA avant le merge, mise en prod. L'agent ne passe aucune porte seul.

Pourquoi ça marche : un agent ne se souvient de rien d'une conversation à l'autre. Tout ce qui n'est pas écrit est perdu. Et un agent qui dit « c'est bon » n'a rien prouvé. Le harness, c'est l'ensemble des fichiers et des habitudes qui compensent ces deux faiblesses.

## L'utiliser en 10 minutes

Il te faut un projet (même vide) dans un dossier, et [Claude Code](https://code.claude.com/docs/en/overview) installé. Un autre agent de code fait l'affaire : les fichiers sont du texte, ils marchent partout.

**Minute 1 à 3. Le contexte.**
Copie `CLAUDE.md.template` à la racine de ton projet, renomme-le `CLAUDE.md`. Remplis les `<…>`. Pas besoin de tout remplir : commence par « Projet », « Commandes de vérification » et « Règles métier ». Claude Code lit ce fichier tout seul à chaque conversation.

Astuce : ouvre Claude Code dans ton projet et demande-lui « lis CLAUDE.md et remplis les sections que tu peux déduire du code, pose-moi des questions pour le reste ».

**Minute 4 à 6. Le skill.**
Copie le dossier `skills/feature/` dans `.claude/skills/feature/` de ton projet (ou dans `~/.claude/skills/feature/` pour l'avoir dans tous tes projets). Relance Claude Code. Tape `/feature` suivi de la description d'un petit ticket.

**Minute 7 à 9. Regarde-le travailler.**
L'agent doit lire le code, puis **s'arrêter** pour te poser ses questions produit. S'il code sans te demander, c'est que le skill n'est pas chargé : vérifie le chemin du dossier.

**Minute 10. La porte.**
Avant de fusionner quoi que ce soit, imprime la [checklist](checklist-portes-humaines.md) et coche. Lis le corps de PR : s'il n'y a pas de section « NON couvert », demande-la.

## Les fichiers

| Fichier | À quoi il sert | Pour qui |
|---|---|---|
| [`README.md`](README.md) | Ce que tu lis. | Tout le monde |
| [`CLAUDE.md.template`](CLAUDE.md.template) | Modèle commenté de la « mémoire » du projet que l'agent lit à chaque session. | Celui qui monte le projet |
| [`checklist-portes-humaines.md`](checklist-portes-humaines.md) | Une page à imprimer : quoi vérifier avant le code, avant le merge, avant la prod. | Tout le monde, surtout les non-codeurs |
| [`skills/feature/SKILL.md`](skills/feature/SKILL.md) | Un skill Claude Code : livrer un ticket de bout en bout, avec les arrêts au bon endroit. | Celui qui pilote l'agent |
| [`exemples/corps-de-pr.md`](exemples/corps-de-pr.md) | Modèle de description de PR honnête : ce qui est fait, ce qui ne l'est pas, ce qui n'est pas vérifié. | Celui qui relit |
| [`exemples/fiche-qa.md`](exemples/fiche-qa.md) | Modèle de fiche de test en tableau. | Celui qui teste |
| [`ressources.md`](ressources.md) | Les articles et docs pour aller plus loin. | Tout le monde |
| [`LICENSE`](LICENSE) | MIT : prends, copie, modifie. | |

## Trois conseils avant de commencer

- **Petit ticket d'abord.** Un bouton, un texte, un filtre. Pas « refais l'authentification ».
- **Une conversation neuve par ticket.** Un agent qui traîne le contexte de trois tickets précédents se trompe plus.
- **Ne mets jamais un vrai secret ou une vraie donnée personnelle dans la conversation.** Ce que l'agent lit peut finir dans un log, un commit ou une PR.

## Licence

MIT, voir [LICENSE](LICENSE). Auteur : Mathis Gorvien.
