## Module 3 – Pull Requests professionnelles

---

### Objectifs pédagogiques

À la fin de ce module, les participants sauront :

✅ Mettre en place une politique de revue claire et automatisée
✅ Utiliser des templates de PR pour faciliter la collaboration
✅ Rédiger des descriptions de PR complètes, structurées et orientées dev/QA/ops
✅ Automatiser l’ajout de labels, reviewers, et règles de protection

---

### Contenu détaillé

---

### 1. **Politique de revue — Professionnaliser le processus**

#### `CODEOWNERS`

> 📌 Permet d’assigner automatiquement des reviewers selon les fichiers modifiés

**Exemple** (`.github/CODEOWNERS`) :

```
# Toute modification dans /api/ devra être validée par l’équipe backend
/api/  @team-backend
/web/  @frontend-lead
*.yml  @devops-team
```

A noter qu'ici on peut egalement indexer uniquement un seul user

- Active l’assignation automatique
- Couplé à la règle "Review required"

#### Protection des branches

> Assure que le merge dans `main` ou `develop` respecte les bonnes pratiques

À activer dans **Settings → Branches → Protection rules** :

- ✅ Require pull request before merging
- ✅ Require review from Code Owners
- ✅ Require status checks to pass
- ✅ Dismiss stale reviews
- ✅ Require linear history (optionnel)

---

### 2. 🧾 **Templates de PR — Standardiser les revues**

> 📄 Un bon template aide à **structurer la communication** autour d'une PR

#### Exemple de fichier : `.github/PULL_REQUEST_TEMPLATE.md`

```md
### Objectif

<!-- Expliquer la finalité de cette PR -->

### Contexte

<!-- Pourquoi ce changement est-il nécessaire ? -->

### Changements apportés

- [x] Implémentation du composant X
- [x] Suppression de l'ancien système Y

### Plan de test

- [x] Test manuel sur Chrome / Safari
- [x] Tests automatisés OK (Jest + Playwright)
- [ ] Vérification sur staging

### Breaking changes ?

- [ ] Oui → nécessite action lors du déploiement
- [x] Non

### Plan de rollback

<!-- Que faire si quelque chose casse en prod ? -->

### Screenshots / Vidéo

<!-- Capture d’écran, démo courte, gif -->
```

> ✅ Ce template sert aux reviewers, aux QA, et parfois même aux ops

---

### 3. 🤖 **Automatisation avec GitHub Actions et outils intégrés**

#### 🔸 Labels dynamiques via `actions/labeler`

> Associe automatiquement des labels selon les fichiers modifiés

**Exemple** (`.github/labeler.yml`) :

```yaml
frontend:
  - "web/**"
backend:
  - "api/**"
tests:
  - "**/*.spec.ts"
docs:
  - "docs/**"
```

**Action associée** :

```yaml
name: Label PRs
on:
  pull_request:
    types: [opened, synchronize, reopened]
jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/labeler@v5
        with:
          repo-token: "${{ secrets.GITHUB_TOKEN }}"
```

#### 🔸 Autres automations utiles

- **GitHub Apps utiles** :

  - [DangerJS](https://danger.systems/) → messages automatiques sur les PR mal formées
  - [Stale bot](https://github.com/actions/stale) → ferme les PR inactives
  - [Semantic Pull Request](https://github.com/amannn/action-semantic-pull-request) → vérifie que le titre respecte Conventional Commits

---

### 4. 📝 **Rédiger une PR efficace — Structure & rigueur**

> 🎯 Objectif : permettre à un reviewer (tech + produit + QA) de comprendre et valider rapidement

#### 🔹 Structure recommandée :

| Partie                   | But                                                      |
| ------------------------ | -------------------------------------------------------- |
| **Contexte**             | Pourquoi ce changement ? Quel ticket ? Quelle urgence ?  |
| **Objectif**             | Ce que la PR est censée accomplir                        |
| **Changements apportés** | Ce que la PR apporte comme changements                   |
| **Plan de test**         | Que doit vérifier le reviewer ? Comment tester ?         |
| **Breaking changes**     | S'il y en a et les mesures a prendre pour le deploiement |
| **Plan de rollback**     | Que faire si on doit annuler en prod ?                   |
| **Risques**              | Casse potentielle, impact sur d’autres systèmes          |
| **Annexes**              | Screenshots, démo vidéo, liens Figma, etc.               |


---

### 🧪 Atelier pratique – « Pull Request Pro »

Objectif : mettre en œuvre tout ce qui précède

#### Étapes à réaliser par les participants :

1. Créer un fichier `.github/PULL_REQUEST_TEMPLATE.md` dans un repo existant
2. Activer une règle de protection sur `main` (review + status checks obligatoires)
3. Ajouter un fichier `CODEOWNERS` avec assignation automatique
4. Installer l’action `actions/labeler` (bonus : ajouter DangerJS ou commit linter)
5. Créer une branche `feature/example-pr`
6. Modifier un fichier, ouvrir une PR avec le **template**, en expliquant :

   - Contexte
   - Ce qui a été changé
   - Plan de test et plan de rollback

7. Demander une review à un binôme

---

### ✅ Résultat attendu

À la fin du lab :

- PR bien formée, avec :

  - Template appliqué
  - Labels générés automatiquement
  - Review requise

- Mise en place des mécanismes de protection

---


# Pourquoi les breaking changes sont importants a signaler

Un **breaking change** (ou **changement rétro-incompatible**) est une modification dans un code, une API, une interface, un schéma, ou un comportement logiciel qui **interrompt ou casse** le fonctionnement pour les utilisateurs existants ou les intégrations déjà en place.

---

### 🧨 Exemples concrets de breaking changes

#### 🔧 En code (API, librairie, backend...)

* Renommer ou supprimer une fonction publique :

  ```ts
  // Ancien
  getUserById(id)

  // Nouveau
  getUser(id) ❌ Breaking si des apps appelaient l'ancienne méthode
  ```
* Changer l’ordre ou le type des paramètres d'une fonction.
* Supprimer un champ dans un JSON retourné par une API REST.
* Modifier le format de réponse (ex : camelCase → snake\_case).
* Introduire une règle ESLint ou TypeScript plus stricte qui empêche le build.

#### 📦 En CI/CD ou outils

* Supprimer un binaire ou une action GitHub utilisée par d'autres workflows.
* Monter une version de Node.js qui casse la compatibilité avec des packages.
* Modifier la structure d'un fichier `.env`, `config.yaml`, etc.

#### 🐘 En base de données

* Renommer ou supprimer une colonne.
* Changer une contrainte (ex : rendre une colonne `NOT NULL` alors qu’elle contenait déjà des `NULL`).
* Changer un enum ou un type sans migration adéquate.

---

### 🚨 Pourquoi c’est critique ?

Parce que **toute personne ou application qui dépendait de l’ancien comportement va planter** ou mal fonctionner, souvent sans prévenir.

> 💡 En versionnage sémantique (`semver`), un breaking change implique un bump **de version majeure** :

```
v2.4.1 → v3.0.0
```

---

### ✅ Comment bien gérer un breaking change

1. **Documenter** précisément ce qui change (changelog).
2. **Prévenir** les utilisateurs à l’avance si possible.
3. **Introduire une période de transition** :

   * Gérer l’ancien et le nouveau comportement en parallèle (déprécation).
   * Ajouter un warning (`console.warn("v1 API will be removed soon")`)
4. **Publier en version majeure**.
5. **Créer un plan de migration clair.**

---

### 🧠 En résumé

| Terme           | Signification                                                |
| --------------- | ------------------------------------------------------------ |
| Breaking change | Modif qui **casse la compatibilité existante**               |
| Safe change     | Ajout ou modification **sans effet sur les usages actuels**  |
| Deprecated      | Ancienne méthode encore supportée, mais **plus recommandée** |

---