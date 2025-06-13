## 🔧 **Module 2 – Bonnes pratiques Git**

---

### 🎯 Objectifs pédagogiques

À la fin de ce module, vous saurez :

✅ Écrire des messages de commit normalisés, utiles pour vos coéquipiers, les changelogs et l’automatisation
✅ Choisir et mettre en œuvre une stratégie de branches efficace (GitFlow, GitHub Flow, Trunk Based Development)
✅ Faire des merges intelligents et utiliser le rebase de manière maîtrisée
✅ Naviguer dans l’historique Git comme un expert pour débugger ou structurer

---

### 📚 Contenu détaillé

---

### 1. 🧾 **Les Conventional Commits — Standardiser les messages**

Structure :

```bash
<type>(optional scope): description courte
```

| Type de commit | Signification                                                    | Exemple                                       |
| -------------- | ---------------------------------------------------------------- | --------------------------------------------- |
| `feat`         | Ajout d’une nouvelle fonctionnalité                              | `feat(auth): enable Google SSO`               |
| `fix`          | Correction d’un bug                                              | `fix(api): correct null response on login`    |
| `docs`         | Ajout ou modification de documentation                           | `docs(readme): add setup instructions`        |
| `style`        | Changement de style (indentation, formatage) sans impact logique | `style: format code with Prettier`            |
| `refactor`     | Refacto de code sans ajout de feature ni correction de bug       | `refactor(user): split service into modules`  |
| `test`         | Ajout ou modification de tests                                   | `test(user): add unit tests for getProfile()` |
| `chore`        | Maintenance, dépendances, build...                               | `chore(deps): upgrade lodash`                 |
| `ci`           | Modifications liées à l'intégration continue                     | `ci(github): add action for testing`          |
| `perf`         | Optimisation de performances                                     | `perf(db): reduce query time on index`        |
| `revert`       | Annule un commit précédent                                       | `revert: feat(auth): enable Google SSO`       |

> 💡 *Pourquoi c’est utile* :
>
> * Lisibilité : historique propre, messages clairs
> * Automation : changelogs auto, version semantique
> * Convention d’équipe partagée

---

### 2. 🧠 **Organisation des branches — Travailler sans chaos**

#### 🌳 **Nommage des branches**

| Préfixe    | Utilisation                                 | Exemple                     |
| ---------- | ------------------------------------------- | --------------------------- |
| `feature/` | Développement d’une nouvelle fonctionnalité | `feature/login-flow`        |
| `fix/`     | Correction d’un bug                         | `fix/reset-password-error`  |
| `hotfix/`  | Urgence en production                       | `hotfix/crash-on-payment`   |
| `release/` | Préparation d’une release versionnée        | `release/1.2.0`             |
| `chore/`   | Maintenance, update de lib, etc.            | `chore/update-dependencies` |
| `test/`    | Expérimentation ou prototypage              | `test/api-stress-test`      |

#### 🧭 **Bonnes pratiques**

* Toujours partir d’une branche stable (`main` ou `dev`)
* Toujours ouvrir une Pull Request pour tout merge
* Supprimer la branche après merge si elle est finie

---

### 3. 🔁 **GitFlow vs GitHub Flow vs Trunk Based**

#### 🔹 **GitFlow** (modèle classique)

* **Branches principales** : `main`, `develop`
* **Branches support** :

  * `feature/*` : dérivées de `develop`
  * `release/*` : dérivées de `develop`, mergées dans `main` et `develop`
  * `hotfix/*` : dérivées de `main`, corrigent un bug urgent
* **Avantages** :

  * Structure claire pour les projets avec livrables versionnés (apps mobiles, packages)
  * Gestion fine des releases
* **Limites** :

  * Trop lourd pour les équipes agiles ou en SaaS

> 🧭 *Diagramme GitFlow :*

```
main <--- hotfix
  ^
   \
  release
     ^
     |
  develop <--- feature
```

---

#### 🔹 **GitHub Flow** (workflow simplifié)

* Basé uniquement sur `main`
* Chaque fonctionnalité part d’une branche courte (ex : `feature/login-form`)
* Merge via PR avec review obligatoire
* Idéal pour les équipes en déploiement continu

> ✅ *Simplicité maximale, rapide et fluide*

---

#### 🔹 **Trunk-Based Development**

* Tout le monde travaille sur une seule branche : `main` (ou `trunk`)
* Feature toggles pour désactiver une fonctionnalité non finalisée
* Déploiement continu automatisé
* Tests automatisés obligatoires avant merge

> ⚠️ Requiert un très bon outillage (CI rapide, feature flags, QA automatisée)

| Critère            | GitFlow              | GitHub Flow             | Trunk-Based Dev     |
| ------------------ | -------------------- | ----------------------- | ------------------- |
| Complexité         | Élevée               | Moyenne                 | Faible              |
| Nombre de branches | 5–6 types            | 1 + features            | 1                   |
| Déploiement        | Manuel ou semi-auto  | CI/CD possible          | CI/CD en continu    |
| Idéal pour         | Logiciels versionnés | Web Apps collaboratives | SaaS, microservices |

---

### 4. 🧬 **Merge vs Rebase — Clarifier les historiques**

| Action          | Description                             | Cas d’usage                   |
| --------------- | --------------------------------------- | ----------------------------- |
| `merge`         | Crée un commit de fusion (merge commit) | Historique clair sur les PR   |
| `rebase`        | Réapplique les commits à une autre base | Historique linéaire, clean    |
| `merge --no-ff` | Forcer un merge commit même si linéaire | Garder une trace des PR       |
| `rebase -i`     | Modifier / fusionner des commits        | Nettoyage avant PR ou release |

> 💡 Conseil :
>
> * En équipe : privilégier **merge** pour garder la clarté des PR
> * En local avant push : **rebase** pour nettoyer

Le **fast-forward** (ou **avancement rapide** en français) est un **type de fusion Git** qui se produit lorsque la branche cible peut être "avancée" directement à la position de la branche source, **sans créer de commit de merge**.

---

### 🔍 En clair :

Si tu as deux branches :

* `main`
* `feature/awesome-feature`

Et que **`main` n’a pas avancé depuis la création de `feature`**, alors le merge peut se faire simplement en déplaçant le pointeur de `main` vers `feature`.

---

### 🧠 Exemple visuel :

```bash
# Historique actuel
A --- B --- C   (main)
           \
            D --- E --- F   (feature)
```

Si `main` n'a pas bougé pendant que `feature` avançait, Git peut juste avancer `main` au même commit que `feature`, **sans créer de commit de fusion** :

```bash
# Après un fast-forward merge
A --- B --- C --- D --- E --- F   (main, feature)
```

---

### 🟢 Avantages

* **Historique plus linéaire** et plus propre
* Pas de commit inutile

---

### 🔴 Inconvénients

* On **perd la trace explicite de la fusion** (il n'y a pas de commit "merge")
* Pas idéal en équipe : difficile de savoir **quelle branche a été fusionnée**

---

### 💡 Bonne pratique en équipe

Quand tu travailles avec des **Pull Requests**, on recommande souvent de **désactiver le fast-forward** pour que chaque merge crée un commit, par exemple avec :

```bash
git merge --no-ff feature/awesome-feature
```

👉 Cela force Git à créer un commit de fusion même si un fast-forward est possible.

---

### 🔧 En résumé

| Type de merge        | Commit de fusion ? | Historique visible ?        | Recommandé pour                 |
| -------------------- | ------------------ | --------------------------- | ------------------------------- |
| Fast-forward         | ❌ Non              | ➖ Non (pas de trace de PR)  | Projets perso, petit historique |
| Merge normal         | ✅ Oui              | ✅ Oui                       | Équipes, PR GitHub              |
| Merge avec `--no-ff` | ✅ Oui              | ✅ Oui (même si FF possible) | CI/CD, audit, release tracking  |


---

### 5. ⚙️ **Commandes et outils avancés**

| Commande        | Utilité                                        |
| --------------- | ---------------------------------------------- |
| `git rebase -i` | Réorganiser, fusionner ou renommer les commits |
| `git stash -p`  | Stasher une portion du code (mode interactif)  |
| `git bisect`    | Trouver le commit fautif par dichotomie        |
| `git mergetool` | Interface visuelle pour résoudre les conflits  |

> ✅ Bonus : configurer VSCode ou Meld comme mergetool

---

### 🧪 Atelier pratique

1. **Configurer Husky + Commitlint**

   * Installation :

     ```bash
     npm install -D husky @commitlint/config-conventional @commitlint/cli
     npx husky install
     ```
   * Ajouter un hook :

     ```bash
     npx husky add .husky/commit-msg 'npx --no -- commitlint --edit $1'
     ```

2. **Créer une branche `hotfix/`**

   * Simuler un bug (ex : crash bouton sur app)
   * Corriger et merger vers `main` avec `--no-ff`

3. **Diagnostiquer un bug avec `git bisect`**

   * Marquer un commit bon :

     ```bash
     git bisect start
     git bisect bad
     git bisect good <sha>
     ```
   * Compiler/tester à chaque étape
   * Git trouve le commit problématique

---

### ✅ Livrables du module

* Repo configuré avec **Husky** et **Commitlint**
* Exemple de branches `feature/`, `hotfix/`, `release/`
* Une PR bien structurée avec `feat(...)`, `fix(...)`
* Utilisation de `bisect`, `rebase`, `stash`, etc.

