# Configuration Claude Code du projet CF2D

Ce dossier est versionné : toute l'équipe partage les mêmes agents, skills et garde-fous.

| Fichier | Rôle | Chargé |
| --- | --- | --- |
| `../CLAUDE.md` | Contexte, commandes, interdits | à chaque session |
| `../frontend/CLAUDE.md` | Règles React | quand Claude travaille dans `frontend/` |
| `MEMORY.md` | Faits durables appris en cours de projet | via `@` dans CLAUDE.md |
| `models.md` | Grille de choix Haiku / Sonnet / Opus | sur demande |
| `agents/*.md` | Sous-agents spécialisés, modèle fixé | quand Claude délègue |
| `skills/*/SKILL.md` | Procédures (`/nouvelle-ressource`, `/verifier`, `/nouvelle-decision`) | sur invocation |
| `settings.json` | Permissions autorisées et interdites | à chaque session |

Préférences personnelles (non versionnées) : `.claude/settings.local.json` et `CLAUDE.local.md`, à ajouter au `.gitignore`.
