# GitHub Workflow Integration Guide

This guide explains how to integrate **GitHub Actions** into your existing project for automated deployment, testing, and CI/CD processes.

---

## 🚀 Step 1: Create `.github/workflows` Directory
1. In your project's root folder, create the following path:

```
/.github/workflows
```

2. Inside this folder, create a new YAML file, e.g., `deploy.yml`.

---

## 📄 Step 2: Write a Basic Workflow
Add the following content to your `.github/workflows/deploy.yml` file:

```yaml
name: 🚀 Deploy Project

on: 
  push:
    branches:
      - main  # Runs on push to the `main` branch

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: 📂 Checkout Code
      uses: actions/checkout@v4

    - name: 📂 Upload via FTP
      uses: SamKirkland/FTP-Deploy-Action@v4.3.5
      with:
        server: ${{ secrets.FTP_SERVER }}
        username: ${{ secrets.FTP_USERNAME }}
        password: ${{ secrets.FTP_PASSWORD }}
        server-dir: "/public_html/"  # Path to deploy files on your FTP server
        local-dir: "./"  # Path to your project's local files
```

---

## 🔒 Step 3: Add Secrets in GitHub
1. Go to your repository on GitHub.
2. Navigate to **Settings** → **Secrets and Variables** → **Actions**.
3. Click the **New repository secret** button.
4. Add the following secrets:
   - `FTP_SERVER` — Your FTP server's IP or domain.
   - `FTP_USERNAME` — The username for the FTP account.
   - `FTP_PASSWORD` — The password for the FTP account.

---

## 🛠️ Step 4: Commit and Push
1. Commit the `.github/workflows/deploy.yml` file to your repository.
2. Push the changes to your remote repository.

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub workflow for FTP deployment"
git push origin main
```

---

## 🚦 Step 5: Monitor Workflow Execution
1. Go to your GitHub repository.
2. Click the **Actions** tab.
3. Select your workflow and view the logs for each step.

---

## ✅ Step 6: Best Practices
- Test your workflow in a staging environment before deploying to production.
- Use conditional checks to prevent accidental deployments (e.g., deploy only when changes are made in specific folders).
- Regularly review your workflow for outdated dependencies or security risks.

---

If you have questions or need custom workflow integration, feel free to ask! 🚀

