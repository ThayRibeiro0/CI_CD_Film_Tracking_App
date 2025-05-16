# CI/CD Tutorial with GitHub Actions and Render

## 🚀 Introduction

This tutorial covers how to set up a basic **CI/CD (Continuous Integration and Continuous Delivery)** flow using **GitHub Actions** and the **Render** deployment service. Ideal for applications with a React front-end and a Node.js back-end with a PostgreSQL database.

---

## 🔁 Explanation of the CI/CD Flow

### What is CI/CD?

- **CI (Continuous Integration)**: Process of continuously testing and integrating code from different collaborators.
- **CD (Continuous Deployment)**: Automated deployment process whenever there are updates to the repository.

---

## ⚙️ How to Configure GitHub Actions

### Create the Workflow Files

Create two files inside your project directory:

```bash
.github/workflows/deploy.yml
.github/workflows/test.yml
```

Add the following configurations to each file (see examples below).

### Add the Render Deploy URL Secret

1. Go to your GitHub repository.
2. Click on **Settings > Secrets and variables > Actions**.
3. Click **New repository secret**.
4. Name: `RENDER_DEPLOY_HOOK_URL`  
5. Value: (Paste the deploy hook URL from Render)

### What Happens After You Push?

- GitHub Actions listens to the `main` branch.
- Then it will:
  1. Check out the repo
  2. Set up Node.js
  3. Install and build the client
  4. Install server dependencies
  5. Trigger the Render deploy

---

## 🌐 How to Configure Render

1. Visit: [https://render.com](https://render.com)
2. Create a **new Web Service**
3. Connect it to your GitHub repository
4. Set your:
   - **Build Command** (e.g., `npm run build`)
   - **Start Command** (e.g., `npm start`)
5. Go to the **Deploy Hooks** section
6. Copy the **Deploy Hook URL**
7. Go back to GitHub and create the `RENDER_DEPLOY_HOOK_URL` secret

---

## 🧾 Example YAML Configurations

### `deploy.yml`

```yaml
name: Deploy to Render on Main
on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger Render Deployment
        run: |
          curl "$RENDER_DEPLOY_HOOK_URL"
        env:
          RENDER_DEPLOY_HOOK_URL: ${{ secrets.RENDER_DEPLOY_HOOK_URL }}
```

---

### `test.yml`

```yaml
name: Cypress Tests on Develop
on:
  pull_request:
    branches:
      - develop

jobs:
  cypress-run:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Dependencies
        run: npm ci
      - name: Run Cypress Tests
        run: npm run test
```

---

## ✅ Summary Flow

1. Developer pushes code or opens a pull request
2. GitHub Actions runs Cypress tests (on `develop`)
3. If merged into `main`, GitHub Actions triggers the deploy
4. Render receives the webhook and deploys the new version automatically
5. 🎉 Live version is updated!

---

## 🔗 Gist Link

Create your Gist at: [https://gist.github.com/](https://gist.github.com/)  