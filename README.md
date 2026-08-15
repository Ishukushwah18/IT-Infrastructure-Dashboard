# 🖥️ IT Infrastructure Dashboard

A simple and responsive **IT Infrastructure Dashboard** built with HTML & CSS and deployed as a static website on **Amazon S3** with an automated **GitHub Actions CI/CD pipeline**.

Every time changes are pushed to the `main` branch, GitHub Actions automatically deploys the latest website files to the S3 bucket.

---

## 🚀 Live Deployment

**Hosting:** Amazon S3
**Region:** `ap-south-1` (Mumbai)

> Add your live website URL here once you have it.

---

## 📸 Project Overview

The dashboard provides a simple interface for monitoring and presenting IT infrastructure information in a clean and organized layout.

### Key Features

* 📊 IT infrastructure dashboard UI
* 💻 Responsive HTML/CSS interface
* ☁️ Amazon S3 static website hosting
* 🔄 Automated CI/CD deployment
* 🔐 GitHub OIDC authentication with AWS
* 🛡️ AWS IAM role-based permissions
* ⚡ Automatic deployment on every push to `main`

---

## 🛠️ Technologies Used

| Technology     | Purpose                       |
| -------------- | ----------------------------- |
| HTML5          | Dashboard structure           |
| CSS3           | Styling and responsive design |
| Git            | Version control               |
| GitHub         | Source code repository        |
| GitHub Actions | CI/CD automation              |
| Amazon S3      | Static website hosting        |
| AWS IAM        | Access control                |
| GitHub OIDC    | Secure AWS authentication     |

---

## 🏗️ Architecture

```text
                👨‍💻 Developer
                     │
                     │ git push
                     ▼
              ┌───────────────┐
              │    GitHub     │
              │   Repository  │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │ GitHub Actions│
              │    CI/CD      │
              └───────┬───────┘
                      │
                      │ OIDC
                      ▼
              ┌───────────────┐
              │    AWS IAM    │
              │   Role        │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │   Amazon S3   │
              │ Static Website│
              └───────┬───────┘
                      │
                      ▼
                  🌐 Live Site
```

---

## 🔄 CI/CD Workflow

The project uses GitHub Actions to automate deployment.

### Deployment Flow

```text
Local Changes
     ↓
git add .
     ↓
git commit
     ↓
git push origin main
     ↓
GitHub Actions
     ↓
AWS OIDC Authentication
     ↓
IAM Role
     ↓
S3 Deployment
     ↓
Live Website Updated 🚀
```

No long-lived AWS Access Keys are stored in the GitHub repository.

---

 AWS Authentication

This project uses **GitHub OIDC (OpenID Connect)** to authenticate GitHub Actions with AWS.

Instead of storing:

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
```

GitHub Actions assumes an AWS IAM role using a temporary OIDC-based session.

IAM Role

```text
GitHubActions-S3-Deploy
```

 AWS Region

```text
ap-south-1
```

S3 Bucket

```text
ishu-it-infrastructure-dashboard-2026
```

---

📁 Project Structure

```text
IT-Infrastructure-Dashboard/
│
├── index.html
├── style.css
│
└── .github/
    └── workflows/
        └── deploy.yml
```

---

 GitHub Actions Workflow

The deployment workflow is triggered whenever code is pushed to the `main` branch.

```yaml
name: Deploy IT Infrastructure Dashboard to S3

on:
  push:
    branches:
      - main

permissions:
  id-token: write
  contents: read

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: arn:aws:iam::744253970642:role/GitHubActions-S3-Deploy
          aws-region: ap-south-1

      - name: Deploy website to S3
        run: |
          aws s3 sync . s3://ishu-it-infrastructure-dashboard-2026 \
            --delete \
            --exclude ".git/*" \
            --exclude ".github/*"
```

> **Security Note:** The IAM Role ARN above is included for documenting the project setup. For public repositories, avoid exposing unnecessary account-specific information and consider replacing it with a placeholder in the README.

---

 Run Locally

Clone the repository:

```bash
git clone https://github.com/Ishukushwah18/IT-Infrastructure-Dashboard.git
```

Navigate into the project:

```bash
cd IT-Infrastructure-Dashboard
```

Open:

```text
index.html
```

in your browser.

---

 Deploy Changes

After making changes locally:

```bash
git add .
git commit -m "Update dashboard"
git push origin main
```

GitHub Actions will automatically deploy the latest version to Amazon S3.

---

What I Learned

Through this project, I gained practical experience with:

* AWS S3 static website hosting
* AWS IAM roles and permissions
* GitHub Actions
* CI/CD pipelines
* GitHub OIDC authentication
* Secure cloud authentication
* Git and GitHub workflow
* Automated cloud deployments

---

🔮 Future Improvements

* Add JavaScript-based live infrastructure metrics
* Add AWS CloudWatch integration
* Add authentication for dashboard access
* Add custom domain with HTTPS
* Add CloudFront CDN
* Improve mobile responsiveness
* Add monitoring and deployment notifications

---
 👨‍💻 Author

Ishu Kushwaha

GitHub:
https://github.com/Ishukushwah18

---

⭐ If you found this project useful, feel free to star the repository!
