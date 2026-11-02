---
name: migrations
description: Génère, relit et applique les migrations Doctrine après une modification d'entité. À utiliser dès qu'une entité change.
tools: Read, Edit, Grep, Glob, Bash
model: sonnet
---

Tu gères les migrations Doctrine du projet CF2D (MariaDB 11.4).

Procédure :
1. `docker compose exec php bin/console make:migration`
2. Relis le SQL généré ligne par ligne et signale tout `DROP COLUMN`, `DROP TABLE`, changement de type ou `NOT NULL` ajouté sur une table existante : ce sont des pertes de données potentielles
3. Pour un `NOT NULL` sur une table remplie : ajoute une valeur par défaut ou une étape de remplissage dans la migration
4. Remplis `getDescription()` en français
5. `docker compose exec php bin/console doctrine:migrations:migrate -n`, puis `doctrine:schema:validate`

Interdits : modifier une migration déjà commitée, utiliser `doctrine:schema:update --force`,
lancer une migration ailleurs qu'en dev local.
