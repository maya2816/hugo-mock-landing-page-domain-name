# Hugo Mock Landing Page - Auto Deployed

## Overview 
This repository contains an **automated deployment pipeline** for a **Hugo static website** using **GitHub Actions** and **GitHub Pages**. 
The site is automatically **built and deployed** whenever changes are pushed to the `main` branch.

This repository is a part of **CIS 3500: Software Engineering**, Homework #2.

---

## 🚀 Workflow Description

This repository uses **GitHub Actions** to automate the deployment process. The workflow is defined in  
📁 **`.github/workflows/gh-pages-deployment.yaml`**.

### **How the GitHub Actions Workflow Works**
1. **Trigger:** The workflow runs **on every push** to the `main` branch.
2. **Checkout Repository:** It fetches the source code from the repository.
3. **Initialize Hugo:** The workflow installs **Hugo** (version `0.144.1`).
4. **Build the Site:** Hugo compiles the static files with options for **minification (`--minify`)** and **garbage collection (`--gc`)**.
5. **Deploy to GitHub Pages:** The compiled site is automatically pushed to the `gh-pages` branch.

### **GitHub Actions Workflow File (`gh-pages-deployment.yaml`)**
```yaml
name: 🏗️ Build and Deploy GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - name: 🔄 Check Out Source Repository
        uses: actions/checkout@v3.5.1
        with:
          submodules: true
          fetch-depth: 0

      - name: 🛠️ Initialize Hugo Environment
        uses: peaceiris/actions-hugo@v2.6.0
        with:
          hugo-version: "0.144.1"
          extended: true

      - name: 🏗️ Compile Hugo Static Files
        run: hugo -D --gc --minify

      - name: 🚀 Publish to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3.9.3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_branch: gh-pages
          user_name: "github-actions[bot]"
          user_email: "github-actions[bot]@users.noreply.github.com"
```

## 🌍 Deployment URL
Once the workflow completes successfully, the website is accessible at:
➡ https://your-github-username.github.io/hugo-mock-landing-page-autodeployed/

## ✅ How to Trigger a New Deployment

To manually trigger a deployment:

1. Make any change in the repository.
2. Commit and push to the main branch.
3. GitHub Actions will automatically rebuild and deploy the website.

**To Verify Deployment:**

* Navigate to the **"Actions"** tab in your repository.
* Click on the most recent workflow run to check **logs and status**.

## 📚 References & Resources
* GitHub Actions Documentation: https://docs.github.com/en/actions
* Hugo Documentation: https://gohugo.io/
* GitHub Pages Setup Guide: https://docs.github.com/en/pages
* peaceiris/actions-gh-pages GitHub Action: https://github.com/peaceiris/actions-gh-pages


