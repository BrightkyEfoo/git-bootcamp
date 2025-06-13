# Quiz avancé Git & GitHub (20 questions)

---

### 1. Quelle est la différence principale entre Git et GitHub ?

a) Git est une plateforme en ligne, GitHub est un outil de gestion de versions
b) Git est un système de gestion de versions décentralisé, GitHub est une plateforme collaborative en ligne
c) GitHub est un langage de programmation, Git est un système de fichiers
d) Aucun des deux

---

### 2. Que signifie un commit de type `feat(auth): enable SSO` ?

a) Correction de bug
b) Ajout d’une nouvelle fonctionnalité dans la partie `auth`
c) Mise à jour de la documentation
d) Refactorisation du code

---

### 3. Parmi ces branches, laquelle correspond au modèle GitFlow ?

a) `main`, `dev`, `feature/*`, `hotfix/*`
b) `master`, `release`, `production`
c) `trunk` uniquement
d) `release/*` et `hotfix/*` uniquement

---

### 4. Quelle est la différence entre `merge` et `rebase` ?

a) `merge` intègre les commits en conservant leur historique, `rebase` réécrit l’historique en déplaçant les commits
b) `rebase` fusionne les branches automatiquement, `merge` les supprime
c) `merge` supprime les branches, `rebase` les crée
d) Aucun des deux

---

### 5. Qu’est-ce qu’un **fast-forward** merge ?

a) Un merge avec conflit
b) Un merge où la branche cible avance simplement le pointeur sans créer de commit de merge
c) Un rebase forcé
d) Un merge qui écrase tous les commits précédents

---

### 6. Quel fichier permet d’assigner automatiquement des reviewers sur GitHub ?

a) `.github/ISSUE_TEMPLATE.md`
b) `.github/CODEOWNERS`
c) `.gitignore`
d) `README.md`

---

### 7. Que fait l’action `actions/labeler` dans un workflow GitHub Actions ?

a) Elle crée des branches automatiquement
b) Elle ajoute des labels dynamiques aux issues ou PR en fonction des fichiers modifiés
c) Elle déploie automatiquement le code
d) Elle compile le code source

---

### 8. Dans un workflow GitHub Actions, que signifie la stratégie `matrix` ?

a) Exécuter un job en parallèle avec différentes variables (ex : versions Node)
b) Sauvegarder les logs de la CI
c) Générer un rapport de test
d) Lancer des scripts shell uniquement

---

### 9. Qu’est-ce qu’un **breaking change** dans le contexte des workflows GitHub Actions ?

a) Une modification qui améliore la performance
b) Une modification incompatible qui peut casser des workflows existants
c) Un commit qui supprime une branche
d) Une correction de bug mineure

---

### 10. Quelle commande permet de retrouver des commits perdus ou supprimés localement ?

a) `git recover`
b) `git reflog`
c) `git reset --hard`
d) `git cherry-pick`

---

### 11. À quoi sert `git cherry-pick` ?

a) Fusionner deux branches
b) Appliquer un commit spécifique d’une branche sur une autre
c) Annuler un commit
d) Cloner un dépôt

---

### 12. Quel est l’avantage principal du squash & merge ?

a) Garder un historique détaillé avec tous les commits
b) Réécrire plusieurs commits en un seul pour un historique propre
c) Supprimer tous les commits d’une branche
d) Annuler un merge

---

### 13. Quel outil permet de tester localement les GitHub Actions ?

a) `gh`
b) `act`
c) `docker-compose`
d) `node`

---

### 14. Quelle commande GitHub CLI permet de créer une Pull Request depuis le terminal ?

a) `gh pr create`
b) `gh pr merge`
c) `gh issue create`
d) `gh repo clone`

---

### 15. Quelles sont les parties d’une version sémantique ?

a) `build.minor.patch`
b) `major.minor.patch`
c) `version.date.commit`
d) `major.patch.minor`

---

### 16. Quel outil génère automatiquement un changelog à partir des messages de commit ?

a) `release-drafter`
b) `commitizen`
c) `standard-version`
d) Les trois sont corrects, avec des usages différents

---

### 17. Quelle est la différence entre une **release** et un **tag** dans GitHub ?

a) Il n’y a aucune différence
b) Un tag est un simple pointeur sur un commit, une release est un tag enrichi avec notes et assets
c) Une release supprime des commits, un tag les conserve
d) Un tag est créé automatiquement, une release manuellement uniquement

---

### 18. Quelles sont les permissions possibles sur un dépôt GitHub ?

a) Read, Write, Execute
b) Observer, Triage, Write, Maintain, Admin
c) Owner, Collaborator, Viewer
d) Basic, Advanced, Admin

---

### 19. Que permet une **Deploy Key** ?

a) Accéder en lecture/écriture à un repo
b) Accéder en lecture seule à un repo pour un serveur de déploiement
c) Créer des branches protégées
d) Supprimer un repo

---

### 20. Que contient un template de Pull Request efficace ?

a) Liste de contrôle des tests
b) Capture d’écran / preuve visuelle
c) Description du contexte, motivation, plan de test, plan de rollback
d) Toutes les réponses précédentes
