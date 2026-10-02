# Workflow Git

- `main` : branche de production. Elle contient uniquement du code validé et stable.
- `dev` : branche d’intégration. Les différentes fonctionnalités y sont regroupées avant leur passage en production.
- `feature/*` : branches éphémères utilisées pour développer les différents livrables ou fonctionnalités.

## Schéma du workflow

```mermaid
gitGraph
   commit id: "init"
   branch dev
   checkout dev
   commit id: "chore: setup"
   branch feat/event-creation
   checkout feat/event-creation
   commit id: "feat: add form"
   commit id: "feat: add validation"
   checkout dev
   merge feat/event-creation id: "PR #1"
   branch fix/date-timezone
   checkout fix/date-timezone
   commit id: "fix: timezone"
   checkout dev
   merge fix/date-timezone id: "PR #2"
   checkout main
   merge dev id: "Release v1.0.0" tag: "v1.0.0"
   branch hotfix/login-crash
   checkout hotfix/login-crash
   commit id: "fix: login crash"
   checkout main
   merge hotfix/login-crash id: "Hotfix" tag: "v1.0.1"
   checkout dev
   merge main id: "Sync hotfix"
```

## Règles

1. Aucun push direct sur `main` ni `dev`.
2. Toute modification passe par une Pull Request.
3. Une PR doit avoir au moins 1 approbation et une CI verte.
4. Les commits respectent Conventional Commits (cf. section précédente).
5. Les branches sont supprimées après merge.
6. Titre de PR au format Conventional Commits (utile avec le squash merge).
7. Merge vers `dev` : squash merge. Merge vers `main` : merge commit (garde la trace des releases).
