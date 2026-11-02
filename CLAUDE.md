# CF2D — Gestion des clients (API Symfony + SPA React)

Plateforme de gestion des clients du CF2D, qui vend du matériel informatique reconditionné.
Public : personnes cherchant du matériel moins cher mais fonctionnel, souvent sur des appareils
anciens ou des connexions lentes. Le frontend doit rester léger et accessible.

**Langue** : tout en français — commentaires, messages de validation, commits, documentation, échanges.

**Stack** : Symfony 7.4 LTS | FrankenPHP | PHP 8.5 | MariaDB 11.4 | Mercure | API Platform | EasyAdmin | React 19 + Vite

Mémoire projet partagée (versionnée) : @.claude/MEMORY.md
Hiérarchie des rôles et permissions : @HIERARCHIE.md

## Architecture

- Symfony = API JSON (`/api`, API Platform) + back-office EasyAdmin (`/admin`). Aucun rendu Twig côté public.
- SPA React dans `frontend/` (règles dans `frontend/CLAUDE.md`). En dev, Vite relaie `/api`, `/admin`
  et `/.well-known/mercure` vers FrankenPHP (`frontend/vite.config.js`).
- FrankenPHP sert l'application directement (pas de nginx ni de php-fpm) et embarque le hub Mercure :
  ne jamais ajouter de conteneur Mercure séparé.

## Environnement Docker (dev)

| Service    | Conteneur  | Accès                    |
| ---------- | ---------- | ------------------------ |
| FrankenPHP | `php`      | http://localhost:8090    |
| Vite       | `frontend` | http://localhost:5174    |
| MariaDB    | `db`       | localhost:3308           |
| phpMyAdmin | `phpmyadmin` | http://localhost:8182  |
| Mailpit    | `mailpit`  | http://localhost:8026    |

## Commandes

Toujours exécuter PHP et Node dans les conteneurs, jamais sur l'hôte :

```bash
docker compose up -d --build
docker compose exec php bin/console <commande>
docker compose exec php composer <commande>

docker compose exec php bin/phpunit                        # tests
docker compose exec php bin/phpunit --filter NomDuTest
docker compose exec php vendor/bin/php-cs-fixer fix        # style (config : .php-cs-fixer.dist.php)

docker compose exec php bin/console make:migration
docker compose exec php bin/console doctrine:migrations:migrate -n
docker compose exec php bin/console doctrine:fixtures:load --group=app -n   # données de test (dev uniquement)

docker compose exec frontend npm run lint
docker compose exec frontend npm run build
```

Raccourcis shell de l'équipe : voir `RACCOURCIS.md` (pour les humains ; Claude utilise les commandes complètes).

Une tâche est terminée quand PHPUnit passe, que php-cs-fixer ne signale rien et que `npm run lint` passe.

## Conventions backend

- Entités : `src/Entity/` — mapping Doctrine en attributs PHP 8, jamais d'annotations
- Exposition API : `#[ApiResource]` sur les entités ; logique spécifique dans `src/State/` (Providers/Processors)
- Logique métier : `src/Service/` — contrôleurs et processors restent minces
- Requêtes : uniquement dans `src/Repository/`
- Autorisations : voters custom dans `src/Security/Voter/`, appliqués via `security:` dans `#[ApiResource]`
- Fixtures : groupe `app` (dev/tests), groupe `prod` (données minimales de production, ex. admin initial)
- Nommage : PascalCase classes, snake_case BDD, camelCase JS

## Branches et déploiement

- `main` : développement
- `preprod/v01` : un push déclenche le déploiement en préproduction (GitHub Actions → SSH VPS)
- `production` : un push déclenche le déploiement en production (VPS Debian 12)

## Interdits

- Ne jamais pousser sur `preprod/*` ou `production`, ni merger vers ces branches, sans demande explicite
- Ne jamais modifier une migration déjà commitée : en créer une nouvelle
- Ne jamais utiliser `doctrine:schema:update --force`
- Ne jamais charger le groupe de fixtures `app` hors du dev local
- Ne jamais lire, modifier ou afficher `.env.local*`, `.env.prod*` ni aucun secret
- Ne jamais écrire d'identifiants ou de mots de passe (même de test) dans la documentation ou le README
- Ne pas ajouter de dépendance Composer ou npm sans l'annoncer et la justifier

## Agents spécialisés

Déléguer aux sous-agents de `.claude/agents/` (règles de choix : `.claude/models.md`) :
- Haiku : `verificateur` (tests + lint), `redacteur-docs`, `admin-crud` (EasyAdmin simple)
- Sonnet : `dev-api`, `dev-react`, `migrations`, `testeur`, `devops`
- Opus : `architecte`, `auditeur-securite`, `debogueur`

Toute modification de code se termine par un passage de `verificateur`.

## Commits

Format : `type(portée): description` en français (ex. `feat(client): filtre par commune`).
Ajouter le trailer `Modele: <haiku|sonnet|opus>`.

## Documentation de référence

À lire seulement quand la tâche le demande :
- Architecture : `docs/architecture/overview.md`
- Schéma BDD : `docs/architecture/database-schema.md`
- Décisions : `docs/architecture/decisions/`
- Docker : `docs/devops/docker-setup.md`
- GitHub Actions : `docs/devops/github-actions.md`
- Déploiement VPS : `docs/devops/vps-preprod.md`
