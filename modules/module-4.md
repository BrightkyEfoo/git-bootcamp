## 🏗️ Module 4 – GitHub Actions CI/CD (4 h)

---

### 🎯 Objectifs pédagogiques

À la fin de ce module, les participants sauront :

✅ Créer des workflows CI/CD robustes et réutilisables
✅ Gérer les secrets et sécuriser les étapes sensibles
✅ Déployer automatiquement via Docker (AWS ECR + ECS)
✅ Générer automatiquement les versions, changelogs et releases

---

### 🧱 1. Architecture d’un Workflow GitHub Actions

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

---

### 🧩 Concepts essentiels

| 🧠 Concept            | 📌 Description                                                               |
| --------------------- | ---------------------------------------------------------------------------- |
| **Jobs / Steps**      | Un **job** contient des **étapes** (steps), s’exécutant sur un runner        |
| **Runners**           | Machine virtuelle (Linux/macOS/Windows) sur laquelle les jobs tournent       |
| **Matrix strategy**   | Permet d’exécuter un job sur plusieurs environnements (ex : Node 18/20/22)   |
| **Cache & Artifacts** | Accélère les builds (cache npm, cache build), partage de fichiers entre jobs |
| **Secrets**           | Variables sensibles stockées dans GitHub (repo, org, env)                    |
| **Triggers**          | `push`, `pull_request`, `workflow_dispatch`, `schedule`, etc.                |
| **Outputs**           | Variables partagées entre steps ou jobs                                      |
| **Environments**      | Contexte pour les secrets spécifiques à un env (staging, prod)               |

---

### ⚙️ 2. Cas pratiques CI/CD

#### 🧪 2.1 – Lint / Test / Build automatique

```yaml
on: [push, pull_request]
jobs:
  lint-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm run lint
      - run: npm run test -- --coverage
      - run: npm run build
```

---

#### 🐳 2.2 – Build & push Docker image vers AWS ECR

```yaml
jobs:
  docker-deploy:
    needs: [lint-test]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      - name: Login to Amazon ECR
        uses: aws-actions/amazon-ecr-login@v2
      - name: Build, tag & push
        run: |
          docker build -t my-app .
          docker tag my-app:latest ${{ secrets.ECR_REGISTRY }}/my-app:latest
          docker push ${{ secrets.ECR_REGISTRY }}/my-app:latest
```

---

#### 🚀 2.3 – Déploiement sur ECS

```yaml
      - name: Deploy to ECS
        uses: aws-actions/amazon-ecs-deploy-task-definition@v1
        with:
          service: my-service
          cluster: my-cluster
          task-definition: my-task-def.json
```

---

#### 🏷️ 2.4 – Release automatisée avec `semantic-release`

> Gère tout : bump de version, changelog, tag, GitHub Release, publication npm...

```yaml
name: Release
on:
  push:
    branches: [main]
jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npx semantic-release
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

---

### 💡 Bonnes pratiques & retours d’expérience

| Pratique                         | Explication                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------- |
| **Build ≠ Deploy**               | Séparer la génération de l’app du déploiement, pour permettre un rollback propre |
| **Principle of Least Privilege** | Donne le minimum de permissions nécessaires à chaque job                         |
| **Reusable Workflows**           | Utilise `workflow_call` pour mutualiser les étapes répétées entre projets        |
| **Matrix combinée**              | Combiner OS + Node + d’autres outils pour tester la compatibilité                |
| **PRs vs Direct Push**           | Restreindre les push directs à `main`, tout doit passer par PR                   |
| **Fail fast / fail clear**       | Arrêter rapidement en cas d’erreur critique (ex : tests échoués)                 |
| **Time-out & Retrys**            | Toujours définir un `timeout-minutes` pour éviter des jobs bloqués               |

---

### 🚨 À anticiper

| Changement GitHub                                     | Impact                                                                                  |
| ----------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `deployments:write` requis à partir du 1er avril 2025 | Tout workflow qui utilise les GitHub Deployments devra avoir des permissions explicites |
| `ubuntu-latest` = Ubuntu 22.04                        | Attention aux breaking changes (ex: Python3 par défaut, changements de libc)            |

```yaml
permissions:
  deployments: write
```

---

### 🔁 Bonus : Reusable workflows

> Pour mutualiser du code dans `.github/workflows/ci.yml` et l’utiliser ailleurs

#### ci.yml (reusable)

```yaml
on:
  workflow_call:
    inputs:
      node-version:
        required: true
        type: string
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ inputs.node-version }}
      - run: npm install
      - run: npm run build
```

#### Utilisation

```yaml
jobs:
  call-ci:
    uses: ./.github/workflows/ci.yml
    with:
      node-version: 20
```

---

### 🧪 Atelier pratique (au choix)

1. Créer un workflow CI pour lint + test un projet Node.js
2. Ajouter un cache pour npm et `node_modules`
3. Déployer une image Docker sur un registre (ECR ou Docker Hub)
4. Publier une release GitHub auto avec `semantic-release`
5. Utiliser un `workflow_call` pour mutualiser build & test entre deux projets

---