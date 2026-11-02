---
name: nouvelle-ressource
description: Crée une nouvelle ressource de bout en bout (entité, migration, API, écran React, tests). À utiliser quand on demande d'ajouter une nouvelle entité métier exposée dans l'application.
---

Enchaîne les agents dans cet ordre, en attendant la fin de chacun :

1. `architecte` : champs, relations, droits par rôle (`HIERARCHIE.md`), opérations API, topics Mercure éventuels.
   Présente le plan à l'utilisateur et attends sa validation avant de continuer.
2. `dev-api` : entité et `#[ApiResource]`
3. `migrations` : migration et application en dev
4. `admin-crud` : écran EasyAdmin, si le plan le prévoit
5. `dev-react` : liste et formulaire dans `frontend/`
6. `testeur` : tests API et composants
7. `verificateur` : rapport final

Termine par un résumé : fichiers créés, routes API, et ce qui reste à faire.
