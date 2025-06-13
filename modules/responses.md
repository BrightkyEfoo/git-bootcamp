### 1. Quelle est la différence principale entre Git et GitHub ?

**Réponse : b)** Git est un système de gestion de versions décentralisé, GitHub est une plateforme collaborative en ligne

---

### 2. Que signifie un commit de type `feat(auth): enable SSO` ?

**Réponse : b)** Ajout d’une nouvelle fonctionnalité dans la partie `auth`

---

### 3. Parmi ces branches, laquelle correspond au modèle GitFlow ?

**Réponse : a)** `main`, `dev`, `feature/*`, `hotfix/*`

---

### 4. Quelle est la différence entre `merge` et `rebase` ?

**Réponse : a)** `merge` intègre les commits en conservant leur historique, `rebase` réécrit l’historique en déplaçant les commits

---

### 5. Qu’est-ce qu’un **fast-forward** merge ?

**Réponse : b)** Un merge où la branche cible avance simplement le pointeur sans créer de commit de merge

---

### 6. Quel fichier permet d’assigner automatiquement des reviewers sur GitHub ?

**Réponse : b)** `.github/CODEOWNERS`

---

### 7. Que fait l’action `actions/labeler` dans un workflow GitHub Actions ?

**Réponse : b)** Elle ajoute des labels dynamiques aux issues ou PR en fonction des fichiers modifiés

---

### 8. Dans un workflow GitHub Actions, que signifie la stratégie `matrix` ?

**Réponse : a)** Exécuter un job en parallèle avec différentes variables (ex : versions Node)

---

### 9. Qu’est-ce qu’un **breaking change** dans le contexte des workflows GitHub Actions ?

**Réponse : b)** Une modification incompatible qui peut casser des workflows existants

---

### 10. Quelle commande permet de retrouver des commits perdus ou supprimés localement ?

**Réponse : b)** `git reflog`

---

### 11. À quoi sert `git cherry-pick` ?

**Réponse : b)** Appliquer un commit spécifique d’une branche sur une autre

---

### 12. Quel est l’avantage principal du squash & merge ?

**Réponse : b)** Réécrire plusieurs commits en un seul pour un historique propre

---

### 13. Quel outil permet de tester localement les GitHub Actions ?

**Réponse : b)** `act`

---

### 14. Quelle commande GitHub CLI permet de créer une Pull Request depuis le terminal ?

**Réponse : a)** `gh pr create`

---

### 15. Quelles sont les parties d’une version sémantique ?

**Réponse : b)** `major.minor.patch`

---

### 16. Quel outil génère automatiquement un changelog à partir des messages de commit ?

**Réponse : d)** Les trois sont corrects, avec des usages différents

---

### 17. Quelle est la différence entre une **release** et un **tag** dans GitHub ?

**Réponse : b)** Un tag est un simple pointeur sur un commit, une release est un tag enrichi avec notes et assets

---

### 18. Quelles sont les permissions possibles sur un dépôt GitHub ?

**Réponse : b)** Observer, Triage, Write, Maintain, Admin

---

### 19. Que permet une **Deploy Key** ?

**Réponse : b)** Accéder en lecture seule à un repo pour un serveur de déploiement

---

### 20. Que contient un template de Pull Request efficace ?

**Réponse : d)** Toutes les réponses précédentes (checklist, screenshots, contexte, motivation, plans)
