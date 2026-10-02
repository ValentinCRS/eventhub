# Eventhub

## Conventions de commit

Nous suivons [Conventional Commits](https://www.conventionalcommits.org/fr/v1.0.0/).

### Format recommandé

```bash
type(scope): description
```

Ou bien, pour une modification avec rupture de compatibilité :

```bash
type(scope)!: description
```

### Structure

- `type` : type de modification
- `scope` : optionnel, précise la zone concernée (ex. `api`, `auth`, `ui`)
- `description` : résumé court et clair en anglais ou français selon le contexte du projet

### Types courants

- `feat` : ajout d’une nouvelle fonctionnalité
- `fix` : correction de bug
- `docs` : mise à jour de la documentation
- `style` : changement de style / formatage sans logique fonctionnelle
- `refactor` : refonte du code sans changement de comportement
- `perf` : amélioration des performances
- `test` : ajout ou modification de tests
- `build` : modification de la configuration de build
- `ci` : modification de la pipeline CI/CD
- `chore` : tâches diverses de maintenance
- `revert` : annulation d’un commit précédent

### Exemples

```bash
feat(auth): add login form
fix(api): correct null response handling
docs: update README for setup instructions
refactor(user): simplify validation logic
test: add unit tests for authentication
```

### Breaking change

Une modification importante doit être signalée avec `!` ou par un footer `BREAKING CHANGE:`.

Exemples :

```bash
feat(api)!: remove legacy endpoint
```

```bash
feat: add new config system

BREAKING CHANGE: environment variables must be renamed
```

### Règles de base

1. Le message doit rester court et explicite.
2. Le type doit refléter la nature du changement.
3. La description doit commencer par une majuscule et rester claire.
4. Les commits doivent rester cohérents pour faciliter le suivi du projet et la génération de changelogs.

### Exemple de commit complet

```bash
feat(ui): add dashboard statistics panel

The dashboard now displays KPIs for user activity and revenue.
The lay
out was adapted for responsive screens.

Reviewed-by: team
Refs: #42
```

---

## Workflow Git

- `main` : branche de production. Elle contient uniquement du code validé et stable.
- `dev` : branche d’intégration. Les différentes fonctionnalités y sont regroupées avant leur passage en production.
- `feature/*` : branches éphémères utilisées pour développer les différents livrables ou fonctionnalités.

### Schéma du workflow

flowchart LR A[feature/*] -->|Pull Request| B[dev] B -->|Pull Request| C[main] C --> D[Production]

### Règles

1. Aucun push direct sur `main` ni `dev`.
2. Toute modification passe par une Pull Request.
3. Une PR doit avoir au moins 1 approbation et une CI verte.
4. Les commits respectent Conventional Commits (cf. section précédente).
5. Les branches sont supprimées après merge.
6. Titre de PR au format Conventional Commits (utile avec le squash merge).
7. Merge vers `dev` : squash merge. Merge vers `main` : merge commit (garde la trace des releases).
