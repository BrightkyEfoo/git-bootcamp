## 📦 Module 5 – Releases & Versioning (1 h)

---

### 🎯 Objectifs pédagogiques

À la fin de ce module, les participants sauront :

✅ Faire la différence entre *tags* et *releases*
✅ Appliquer le versioning sémantique (SemVer) de manière cohérente
✅ Mettre en place un système automatique de génération de changelog
✅ Intégrer la publication de releases dans un pipeline CI/CD

---

### 🔖 1. Tags vs Releases

| Élément            | Description                                                                                                                      |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| **Tag Git**        | Un pointeur vers un commit précis. Utilisé pour marquer une version stable. Exemple : `v1.2.0`                                   |
| **Release GitHub** | Une release enrichie avec : titre, description (changelog), fichiers attachés, notes de publication. Elle est associée à un tag. |

> 💡 Tous les tags ne sont pas des releases GitHub, mais toute release GitHub est basée sur un tag.

---

### 🧮 2. Version sémantique (SemVer)

Le versionnage **MAJOR.MINOR.PATCH** permet de communiquer clairement la nature d’un changement.

| Type    | Exemple         | Description                                   |
| ------- | --------------- | --------------------------------------------- |
| `MAJOR` | `1.0.0 → 2.0.0` | Rupture de compatibilité (breaking change)    |
| `MINOR` | `1.2.0 → 1.3.0` | Nouvelles fonctionnalités **compatibles**     |
| `PATCH` | `1.2.3 → 1.2.4` | Corrections de bugs ou améliorations internes |

> 📌 Bonnes pratiques :
>
> * Les versions doivent **toujours** commencer par `v` (`v1.0.0`)
> * Les *breaking changes* doivent être **expliqués** dans les notes de version

---

### 🧰 3. Outils utiles

| Outil                | Fonction principale                                                     |
| -------------------- | ----------------------------------------------------------------------- |
| **Release Drafter**  | Génère automatiquement les notes de version à partir des PR labellisées |
| **standard-version** | Incrémentation de version + changelog local depuis les commits          |
| **semantic-release** | CI intégrale : version + changelog + tag + GitHub release + npm publish |

---

### 🔄 4. Processus recommandé

1. **Merge PR** dans `main` ou `release/*`
2. **GitHub Actions** déclenche :

   * Tests
   * Build
   * Création ou mise à jour du draft de release
3. **Mainteneur** relit, ajuste, puis publie la release
4. La **publication** peut déclencher :

   * Déploiement
   * Notification Slack/Discord
   * Publication sur npm, Docker Hub…

---

### 🚧 5. Exemple de Release Drafter

> Fichier `.github/release-drafter.yml`

```yaml
name-template: 'v$RESOLVED_VERSION'
tag-template: 'v$RESOLVED_VERSION'
version-resolver:
  major:
    labels:
      - 'breaking'
  minor:
    labels:
      - 'feature'
  patch:
    labels:
      - 'fix'
  default: patch

categories:
  - title: '🚨 Breaking Changes'
    labels:
      - 'breaking'
  - title: '✨ Features'
    labels:
      - 'feature'
  - title: '🐛 Fixes'
    labels:
      - 'fix'
  - title: '📦 Dependencies'
    labels:
      - 'dependencies'
  - title: '🧹 Maintenance'
    labels:
      - 'chore'

template: |
  ## 📝 Notes de version
  $CHANGES
```

> Active ensuite l’action avec un workflow `.github/workflows/release-drafter.yml` :

```yaml
name: Release Drafter
on:
  push:
    branches:
      - main
  pull_request:
    types: [closed]

jobs:
  update_release_draft:
    runs-on: ubuntu-latest
    steps:
      - uses: release-drafter/release-drafter@v6
        with:
          config-name: release-drafter.yml
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

---

### 🧪 Atelier pratique

1. Ajouter un fichier `.github/release-drafter.yml` dans un repo de test
2. Créer des PR labellisées `feature`, `fix`, `breaking`, etc.
3. Observer la génération automatique du *draft release*
4. Publier manuellement une release depuis GitHub


## 📦 Qu’est-ce qu’une *Release* ?

Une **release** est une **version officielle et distribuable** d’un logiciel ou d’un projet.

Elle sert à **publier un état stable** de ton code, souvent pour la mise en production ou la distribution aux utilisateurs.

---

### Différences entre *Tag* et *Release*

* **Tag** :

  * C’est un pointeur statique sur un commit spécifique dans Git.
  * Il marque un point dans l’historique (par exemple, `v1.0.0`).
  * Il est simple, sans métadonnées supplémentaires.

* **Release GitHub** :

  * C’est un **tag enrichi** avec :

    * Un titre
    * Une description détaillée (notes de version ou changelog)
    * Des fichiers joints (assets) comme des exécutables, des binaires, des archives ZIP/ZIP, des packages
    * Un suivi visible sur GitHub avec la possibilité de télécharger les assets
  * Elle sert à informer les utilisateurs et développeurs des nouveautés, corrections, et changements majeurs.

---

### Pourquoi créer une release ?

* Pour **communiquer officiellement** la disponibilité d’une version stable
* Pour **distribuer facilement** des fichiers binaires, installateurs, ou bundles
* Pour **documenter** les changements apportés depuis la dernière version (changelog)
* Pour **faciliter la traçabilité** des versions en production

---

### Exemple concret

Quand un projet atteint un jalon important (ex : fin d’une fonctionnalité majeure), on crée une release `v2.0.0` qui contient :

* Le code à ce stade
* Un résumé des nouveautés, corrections, bugs connus
* Les fichiers téléchargeables prêts à être installés ou déployés

---

### En résumé

> **Une release est la manière “officielle” de publier une version de ton projet, avec un tag Git enrichi d’informations et fichiers pratiques pour les utilisateurs.**

