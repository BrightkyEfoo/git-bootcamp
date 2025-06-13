# 🧠 Bootcamp GitHub Avancé – Maîtriser GitHub comme un Bright

---
  ##Billy boy participated in this wonderful bootcamp
## Prérequis

* Maîtriser les commandes Git de base (clone, commit, merge, rebase)
* Compte GitHub avec droits « Write » sur un dépôt d’entraînement
* Node LTS & Docker installés localement (pour les labs CI/CD)

---

## Module 1 – Introduction (1 h)

### Objectifs pédagogiques

* Distinguer Git (VCS) et GitHub (plateforme collaborative)
* Définir clairement les objectifs & livrables du bootcamp
* Explorer les cas d’usage modernes : CI/CD, revue de code, sécurité

### Contenu détaillé

1. **Git vs GitHub :** architecture décentralisée vs services managés (PR, Actions, Packages)
2. **Cas d’usage concrets :** pipeline multi‑cloud, policy CODEOWNERS, analyse de vulnérabilités
3. **Démo express :** Fork → clone → Pull Request → merge → déploiement (Vercel)

### Atelier « Ice‑breaker »

Chaque participant corrige une faute de frappe dans le README du dépôt de démonstration et ouvre sa première PR.

---

## Module 2 – Bonnes pratiques Git (2 h)

### Objectifs

* Structurer un historique de commits lisible & exploitable
* Choisir une stratégie de branches adaptée au produit

### Points clés

| Sujet                         | Contenu                                                        | Exemple / Outil          |
| ----------------------------- | -------------------------------------------------------------- | ------------------------ |
| **Conventional Commits**      | `<type>(scope): message`                                       | `feat(auth): enable SSO` |
| **Changelog auto**            | *commitizen*, *cz‑conventional‑changelog*                      | `npm run commit`         |
| **Organisation des branches** | `main`, `dev`, `feature/*`, `hotfix/*`                         | Diagramme GitFlow        |
| **GitFlow vs Trunk Based**    | Avantages, limites, contextes                                  | Release mobile vs SaaS   |
| **Astuces pro**               | `git rebase -i`, `git stash -p`, `git bisect`, `git mergetool` | Démo live                |

### Atelier pratique

1. Configurer Husky + Commitlint pour imposer les messages de commit.
2. Simuler un bug production et le corriger via une branche *hotfix/*.
3. Utiliser `git bisect` pour isoler un commit fautif.

---

## Module 3 – Pull Requests professionnelles (1 h 30)

* **Politique de revue** : assignation automatique via CODEOWNERS, règle « Review required »
* **Templates de PR** : checklist de tests, screenshots, breaking changes
* **Automatisation** : labels dynamiques (`actions/labeler`), protection de branche
* **Rédaction efficace** : contexte ► motivation ► plan de test ► plan de rollback

### Lab

Créer `.github/PULL_REQUEST_TEMPLATE.md`, activer les règles de protection, puis ouvrir une PR exemple.

---

## Module 4 – GitHub Actions CI/CD (4 h)

### Architecture d’un workflow

```yaml
name: CI
on:
  push:
    branches: [main, dev]
jobs:
  build-test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node: [18, 20, 22]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
      - run: npm ci
      - run: npm test -- --coverage
      - uses: actions/cache@v4
        with:
          path: ~/.npm
          key: ${{ runner.os }}-${{ hashFiles('package-lock.json') }}
```

### Concepts essentiels

* **Jobs / Steps / Runners**
* **Matrix Strategy** : tests parallèles multi‑environnements
* **Caching & Artifacts**
* **Secrets** : repository, environment, organisation

### Cas pratiques

1. **Lint/Test/Build** automatisés sur `push`.
2. **Déploiement Docker** → AWS ECR puis ECS.
3. **Release** via *semantic‑release* : version, tag, notes, publication GitHub Release.

### Bonnes pratiques

* Séparer build & deploy, principe du *least privilege*.
* **Reusable workflows** via `workflow_call` (20 workflows max, 4 niveaux de nesting).
* Anticiper les *breaking changes* GitHub Actions (ex. `deployments:write` requis dès **01‑04‑2025**).

---

## Module 5 – Releases & Versioning (1 h)

* **Tags vs Releases** : métadonnées, assets, changelog
* **Version sémantique** MAJOR.MINOR.PATCH
* Outils : *release‑drafter*, *standard‑version*
* Processus : merge PR → pipeline CI → draft release → validation

### Atelier

Configurer *release‑drafter* pour générer automatiquement les notes de version depuis les labels de PR.

---

## Module 6 – Sécurité, accès & environnements (1 h 30)

* **Rôles GitHub** : Observer, Triage, Write, Maintain, Admin
* **Teams & Groups** pour la délégation
* **CODEOWNERS** sur le code sensible
* **Deploy Keys vs Fine‑grained PAT**
* **Environments** : variables & secrets segmentés, approbations obligatoires

### Lab

Créer un environment *production* avec double approbation et secrets dédiés.

---

## Module 7 – Astuces avancées (1 h 30)

* Résolution de conflits complexes (`git mergetool`, meld, vscode)
* Extraction ciblée de commits : `git cherry‑pick`
* Restauration d’historique : `git reflog`
* **Squash & Merge** sans polluer l’historique
* **GitHub CLI** (`gh`) : `gh pr create`, `gh run watch`, `gh release create`
* Tester les Actions localement avec **act**

---

## Module 8 – Démo finale & Q/R (1 h)

1. Cycle complet : Branch → PR → Review ► Merge → CI → Release → Déploiement.
2. Session questions/réponses & partage d’expériences.
3. Roadmap d’implémentation post‑bootcamp.

---

## Annexes

### Cheatsheets

* Commandes Git : log, rebase, bisect
* Référence YAML GitHub Actions
* SemVer & Conventional Commits

### Références clés

* GitHub Docs – Reusing Workflows
* GitHub Blog – Breaking Changes 03‑2025
* Conventional Commits – Spécification officielle
* Matrix Strategy – Codefresh guide

### Évaluation

* **Quiz** 20 questions (Kahoot)
* **Challenge final** : configurer un pipeline CI + Semantic release sur un dépôt forké.