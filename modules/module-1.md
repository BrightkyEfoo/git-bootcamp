## 🎓 **Module 1 – Introduction**

---

### 🎯 Objectifs pédagogiques

À la fin de ce module, les participants seront capables de :

✅ Faire la différence entre Git (outil de versionnage) et GitHub (plateforme de collaboration)
✅ Comprendre les objectifs du bootcamp et les livrables attendus
✅ Identifier les cas d’usage avancés de GitHub en entreprise : automatisation, sécurité, collaboration

---

### 📚 Contenu détaillé

#### 1. 🔄 **Git vs GitHub**

|                     | Git                                        | GitHub                                                        |
| ------------------- | ------------------------------------------ | ------------------------------------------------------------- |
| **Type**            | Outil de versionnage distribué (VCS)       | Plateforme de collaboration autour de Git                     |
| **Installation**    | Local sur chaque machine                   | Plateforme en ligne (cloud)                                   |
| **Fonctions clés**  | commit, branch, merge, stash, rebase, etc. | Pull Request, Issues, Actions, Pages, Releases, Environments  |
| **Usage principal** | Historique local de version                | Travail collaboratif, intégration continue, gestion des accès |

> 📝 Exemple : Git = écrire ton texte en local, GitHub = Google Docs avec commentaires + historique + publication automatique.

---

#### 2. 💼 **Cas d’usage concrets de GitHub aujourd’hui**

* **CI/CD multiplateforme** :

  * Tests automatisés sur plusieurs environnements
  * Déploiement vers Vercel, Netlify, AWS, Firebase, etc.
* **Gestion de code collaborative** :

  * Relecture obligatoire (Pull Requests)
  * Gestion des droits et des rôles
  * `CODEOWNERS` pour forcer la revue d’équipes spécifiques
* **Sécurité intégrée** :

  * Détection de secrets dans le code
  * Analyse des dépendances via Dependabot
  * Vérification des tokens et permissions dans les workflows
* **Exemples en entreprise** :

  * Changelog automatique à chaque release
  * Publication de packages dans GitHub Packages
  * Documentation auto-déployée avec GitHub Pages

---

#### 3. ⚡ **Démo express** *(5–10 minutes)*

1. Fork d’un dépôt de démo public
2. Clone en local (`git clone`)
3. Création d'une branche (`git checkout -b fix/typo`)
4. Modification du README.md (petite faute de frappe)
5. Commit et push (`git commit -m "fix: typo in README"`)
6. Ouverture d’une Pull Request via l’interface GitHub
7. Merge une fois validée → déploiement automatique déclenché (Vercel)

github: https://github.com/BrightkyEfoo/parallax
link: https://parallax-nine-psi.vercel.app/parallax-mountain

---

### ❄️ **Atelier Ice-breaker – PR express**

**Objectif** : chaque participant entre dans l’action dès les premières minutes.

* Un dépôt de démonstration contient **5 à 10 fautes de frappe** volontairement insérées dans le README.
* Chaque participant :

  * Fork le dépôt
  * Corrige une faute
  * Crée une branche
  * Push et ouvre sa **première Pull Request**
  
* Discussion rapide autour :

  * Des messages de commit
  * De la branche utilisée
  * De l’expérience sur l’interface GitHub

---

### ✅ Livrables du module

* ✅ Un dépôt forké propre
* ✅ Une PR créée et (si approuvée) mergée
* ✅ Un premier aperçu de CI/CD si le projet est branché à Vercel
* ✅ Une compréhension claire de ce qu’est Git, GitHub, et ce que vous apprendrez ensuite
