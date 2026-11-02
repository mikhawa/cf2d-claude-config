# Frontend — SPA React 19 + Vite

Complète le CLAUDE.md racine. S'applique à `frontend/`.

## Commandes (dans le conteneur `frontend`)

```bash
docker compose exec frontend npm run lint
docker compose exec frontend npm run build
docker compose exec frontend npm test
```

Le serveur Vite tourne déjà dans le conteneur (http://localhost:5174) : ne pas le relancer.

## Conventions

- Composants fonctionnels uniquement, un composant par fichier, nom en PascalCase (`ClientCard.jsx`)
- Hooks personnalisés dans `src/hooks/`, préfixés `use`
- Appels API centralisés dans `src/api/` : aucun `fetch` directement dans un composant
- Toujours des URL relatives (`/api/...`) : le proxy Vite en dev et FrankenPHP en prod s'en chargent
- Temps réel : `EventSource` sur `/.well-known/mercure`, encapsulé dans un hook dédié
- Textes affichés en français

## Contraintes

- Public sur matériel ancien : pas de bibliothèque lourde, routes chargées en `lazy`
- Accessibilité : labels sur tous les champs, navigation clavier, contrastes suffisants
- Les droits sont vérifiés par l'API : le frontend masque, il ne sécurise jamais
- Ne jamais stocker de jeton dans `localStorage` (cookie HttpOnly posé par l'API)
