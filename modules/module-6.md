## 🔐 Module 6 – Sécurité, accès & environnements (1 h 30)

---

### 🎯 Objectifs pédagogiques

À l’issue de ce module, les participants sauront :

* Comprendre et configurer les rôles et permissions dans GitHub
* Organiser les équipes pour déléguer les accès
* Protéger les parties sensibles du code avec CODEOWNERS
* Différencier les méthodes d’accès automatisé : Deploy Keys vs Fine-grained PAT
* Gérer les environnements GitHub avec secrets, variables et validations

---

### 1. Rôles GitHub

GitHub propose 5 rôles standards au niveau dépôt, qui déterminent le niveau d’accès :

| Rôle         | Permissions principales                          | Usage typique                 |
| ------------ | ------------------------------------------------ | ----------------------------- |
| **Observer** | Lecture seule, accès limité                      | Auditeurs, observateurs       |
| **Triage**   | Lecture + gestion issues/PR sans push            | Gestionnaires QA, modérateurs |
| **Write**    | Lecture + push direct sur branches               | Développeurs                  |
| **Maintain** | Write + gestion des paramètres et de la sécurité | Leads techniques, managers    |
| **Admin**    | Contrôle total (paramètres, accès, suppression)  | Admins, responsables sécurité |

> 💡 Le rôle `Triage` est souvent méconnu mais très utile pour déléguer la gestion des issues/PR sans risque d’altération du code.

---

### 2. Teams & Groups

* **Groupes d’utilisateurs** permettant de gérer les accès par équipe plutôt qu’individuellement.
* On peut assigner des rôles à des équipes pour simplifier la gestion.
* Exemples d’équipes :

  * Frontend
  * Backend
  * DevOps
  * Support

> 🛠️ Astuce : Intégrer l’authentification SSO (ex : via GitHub Enterprise) pour gérer la sécurité globale.

---

### 3. CODEOWNERS

* Fichier `.github/CODEOWNERS` pour désigner les responsables d’un dossier ou fichier.
* Les reviewers sont automatiquement assignés sur les PR qui modifient ces fichiers.
* Syntaxe :

```plaintext
# Assigner une équipe à un dossier
/docs/ @doc-team

# Assigner un utilisateur à un fichier spécifique
/config/secret.yml @username
```

> ✅ Permet d’assurer une revue ciblée sur les parties critiques (ex : sécurité, infra, API).

---

### 4. Deploy Keys vs Fine-grained Personal Access Tokens (PAT)

| Accès       | Deploy Key                                  | Fine-grained PAT                                    |
| ----------- | ------------------------------------------- | --------------------------------------------------- |
| Usage       | Clonage/push automatisé pour un repo unique | Accès contrôlé sur plusieurs repos ou organisations |
| Permissions | En lecture seule ou en lecture/écriture     | Permissions détaillées par scope                    |
| Portée      | Un seul dépôt                               | Organisation entière ou ensemble de dépôts          |
| Rotation    | Manuelle via gestion des clés SSH           | Plus facile via GitHub UI/API                       |

> 🔐 **Deploy Keys** sont idéales pour les CI/CD avec accès restreint.
> 🔑 **Fine-grained PAT** offrent plus de flexibilité pour les robots ou services.

---

### 5. Environments GitHub

* **Définition** : Espaces dédiés (ex : `production`, `staging`) avec secrets et variables spécifiques.
* **Fonctionnalités clés** :

  * Secrets isolés par environnement
  * Protection avec règles d’approbation (reviewers requis)
  * Restrictions sur les branches pouvant déployer vers cet environnement

> 🔄 Exemples d’usage :
>
> * Protéger la prod avec double approbation avant déploiement
> * Variables différentes selon l’environnement (API keys, URLs)

---

### 🧪 Lab pratique

1. Créer un environment `production` dans les paramètres du repo
2. Ajouter au moins deux secrets (`PROD_API_KEY`, `DB_PASSWORD`) à cet environment
3. Configurer l’environnement pour exiger une double approbation (minimum 2 reviewers) avant déploiement
4. Mettre à jour un workflow GitHub Action pour utiliser ce environment et ses secrets
5. Simuler un déploiement qui bloque tant que les approbations ne sont pas validées
