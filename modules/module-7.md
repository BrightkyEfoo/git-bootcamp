## 🚀 Module 7 – Astuces avancées

---

### 🎯 Objectifs pédagogiques

À la fin de ce module, les participants pourront :

* Gérer et résoudre efficacement des conflits complexes
* Extraire et manipuler des commits spécifiques
* Restaurer l’historique en cas d’erreurs
* Maintenir un historique clair avec squash & merge
* Utiliser la CLI GitHub pour automatiser et simplifier les workflows
* Tester les workflows GitHub Actions localement

---

### 1. Résolution de conflits complexes

* **Conflits fréquents** lors du merge ou du rebase
* Utilisation d’outils graphiques pour faciliter la résolution :

  * `git mergetool` (interface configurable)
  * Outils recommandés : **meld**, **VSCode** (intégration Git)
* Exemples pratiques : détection des conflits, édition manuelle, validation

---

### 2. Extraction ciblée de commits : `git cherry-pick`

* Permet de **reprendre un ou plusieurs commits précis** d’une branche et les appliquer sur une autre
* Utile pour backporter un fix critique sans merger toute la branche
* Syntaxe :

  ```bash
  git cherry-pick <commit-hash>
  ```
* Gestion des conflits possible lors du cherry-pick

---

### 3. Restauration d’historique : `git reflog`

* **Reflog** : journal local de toutes les modifications de HEAD
* Permet de récupérer des commits ou branches même après un reset ou un rebase raté
* Exemple :

  ```bash
  git reflog
  git checkout <sha> 
  ```
* Très utile en cas de suppression accidentelle

---

### 4. Squash & Merge

* Technique pour **combiner plusieurs commits en un seul** lors d’un merge
* Permet de garder un historique propre, lisible et éviter la pollution par de multiples petits commits (ex : fix typo, debug)
* Pratique sur GitHub via l’option “Squash and merge” dans les Pull Requests
* Conseils pour bien rédiger le message du commit squash

---

### 5. GitHub CLI (`gh`)

* Outil en ligne de commande puissant pour interagir avec GitHub
* Commandes utiles :

  * `gh pr create` : créer une Pull Request depuis le terminal
  * `gh run watch` : suivre l’exécution des workflows GitHub Actions en temps réel
  * `gh release create` : créer une release GitHub en ligne de commande
* Installation simple, gain de temps pour les workflows automatisés

---

### 6. Tester les GitHub Actions localement avec **act**

* `act` est un outil open-source qui simule l’exécution des GitHub Actions sur ta machine
* Permet de tester rapidement ses workflows sans pousser sur GitHub
* Installation via `brew` / `apt` / `choco` ou binaire
* Commandes de base :

  ```bash
  act -j <job-name>
  ```
* Idéal pour déboguer et itérer rapidement

---

### 🧪 Atelier pratique

* Résoudre un conflit complexe sur un merge avec `git mergetool` (VSCode ou meld)
* Cherry-pick un commit spécifique d’une autre branche
* Utiliser `git reflog` pour récupérer un commit perdu
* Faire un squash & merge localement avec `git rebase -i`
* Créer une PR et une release via `gh` en CLI
* Installer et lancer `act` pour simuler un workflow simple
