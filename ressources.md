# Ressources

Tous les liens ont été vérifiés le 6 novembre 2026. La plupart sont en anglais.

## Comprendre les agents et le harness

- [Building effective AI agents](https://www.anthropic.com/research/building-effective-agents) (Anthropic). Le point de départ : workflows contre agents, et pourquoi commencer simple.
- [Effective harnesses for long-running agents](https://www.anthropic.com/research/effective-harnesses-for-long-running-agents) (Anthropic). Comment un agent reprend le travail avec un contexte vide : un fichier de progression et l'historique git.
- [Harness design for long-running apps](https://www.anthropic.com/research/harness-design-long-running-apps) (Anthropic). La suite : un rôle de planificateur, et repartir d'un contexte neuf plutôt que de compresser.
- [Effective context engineering for AI agents](https://www.anthropic.com/research/effective-context-engineering-for-ai-agents) (Anthropic). Le contexte est une ressource limitée : quoi y mettre, quand, et comment.
- [How we built our multi-agent research system](https://www.anthropic.com/research/multi-agent-research-system) (Anthropic). Un orchestrateur et des sous-agents, avec les erreurs rencontrées.

## Claude Code

- [Vue d'ensemble](https://code.claude.com/docs/en/overview) : installer et démarrer.
- [Bonnes pratiques](https://code.claude.com/docs/en/best-practices) : la méthode recommandée par Anthropic.
- [Mémoire et CLAUDE.md](https://code.claude.com/docs/en/memory) : où placer le fichier, comment il est chargé.
- [Skills](https://code.claude.com/docs/en/skills) : écrire un `SKILL.md` comme celui de ce kit.
- [Sous-agents](https://code.claude.com/docs/en/sub-agents) : l'éclaireur, l'exécutant, le conseiller.
- [Hooks (guide)](https://code.claude.com/docs/en/hooks-guide) et [hooks (référence)](https://code.claude.com/docs/en/hooks) : des contrôles automatiques avant ou après chaque action de l'agent.
- [MCP dans Claude Code](https://code.claude.com/docs/en/mcp) : brancher l'agent sur tes outils (backlog, base, design).
- [Workflows courants](https://code.claude.com/docs/en/common-workflows) : dont le travail en parallèle avec les worktrees.
- [Model Context Protocol](https://modelcontextprotocol.io/) : le standard ouvert derrière MCP.

## Git

- [git worktree](https://git-scm.com/docs/git-worktree) : plusieurs copies de travail d'un même dépôt, une par ticket. C'est ce qui permet de faire tourner plusieurs agents sans qu'ils se marchent dessus.
- [GitHub CLI](https://cli.github.com/) : ouvrir une PR depuis le terminal (`gh pr create`). L'agent s'en sert.

## Les outils du setup

- [Claude Code](https://www.claude.com/product/claude-code) : l'agent de code.
- [Orca](https://www.onorca.dev/) ([code source](https://github.com/stablyai/orca)) : une app pour faire tourner plusieurs agents en parallèle, chacun dans son worktree.
- [Notion](https://www.notion.com/) : le backlog et les fiches QA.
- [GitHub](https://github.com/) : le code, les PR, la CI.
- [Supabase](https://supabase.com/) : base Postgres, auth, stockage. À lire : [Row Level Security](https://supabase.com/docs/guides/database/postgres/row-level-security), les droits au niveau de la base.
- [Vercel](https://vercel.com/) : hébergement du front.
- [Render](https://render.com/) : hébergement du back.
- [Figma](https://www.figma.com/) : les maquettes.
