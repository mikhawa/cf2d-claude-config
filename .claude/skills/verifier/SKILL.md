---
name: verifier
description: Vérifie que le projet est prêt à être commité (tests, style, lint, build). À utiliser avant un commit ou quand l'utilisateur demande si tout est en ordre.
---

1. Délègue à `verificateur`.
2. Si tout est OK, lance `docker compose exec frontend npm run build`.
3. Si des fichiers dans `src/Entity/` ont changé (`git status`), vérifie qu'une migration correspondante existe dans `migrations/`.
4. Propose un message de commit au format `type(portée): description`, avec le trailer `Modele:`.

Ne commite pas toi-même.
