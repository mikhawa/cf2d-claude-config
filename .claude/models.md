# Choix du modèle et délégation

Le modèle de la session principale est choisi par l'humain (`/model`). Claude ne change pas de modèle
lui-même : il délègue à un sous-agent dont le modèle est fixé dans son fichier `.claude/agents/*.md`.

## Grille de décision

| Critère | Haiku | Sonnet | Opus |
| --- | --- | --- | --- |
| Fichiers touchés | 1–2 | plusieurs, un seul domaine | transversal (API + React + infra) |
| Risque | nul (lecture, doc, style) | moyen (logique métier, schéma BDD) | élevé (sécurité, données, architecture) |
| Réflexion | exécuter une procédure | appliquer des conventions connues | arbitrer entre plusieurs options |
| Réversibilité | immédiate | via git | coûteuse (migration en prod, contrat d'API) |

En cas de doute entre deux niveaux, prendre le niveau supérieur pour l'analyse et le niveau inférieur pour l'exécution.

## Enchaînements types

- Nouvelle fonctionnalité : `architecte` (plan) → `migrations` → `dev-api` → `dev-react` → `testeur` → `verificateur`
- Bug simple : `dev-api` ou `dev-react` → `verificateur`
- Bug incompris après une tentative : `debogueur`
- Avant un merge vers `preprod/v01` : `auditeur-securite` → `verificateur`

## Traçabilité

Le modèle utilisé est indiqué par le trailer de commit `Modele: <haiku|sonnet|opus>`.
