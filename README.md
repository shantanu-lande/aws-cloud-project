# AWS Automated Cloud Deployment & CI/CD Pipeline

![AWS S3](https://img.shields.io/badge/AWS-S3-orange?style=for-the-badge&logo=amazons3)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-blue?style=for-the-badge&logo=githubactions)
![DevOps](https://img.shields.io/badge/DevOps-Automated_Deployment-green?style=for-the-badge&logo=devops)

An automated Continuous Integration and Continuous Deployment (CI/CD) pipeline that deploys a static website to **Amazon S3** using **GitHub Actions**. Every `git push` to the `main` branch automatically authenticates with AWS, syncs repository updates, and updates the live web application within seconds.

---

## 🌟 Project Overview

Manual application deployments via web consoles or direct FTP uploads introduce human error, lack auditability, and cause downtime. This project implements a modern DevOps strategy using **Infrastructure-as-Code (IaC)** concepts to automate static web hosting.

### Key Architecture & Data Flow

```text
[ Developer Push ] ──> [ GitHub Repository ] ──> [ GitHub Actions Runner ]
                                                         │
                                               (IAM Authenticated)
                                                         │
                                                         ▼
                                             [ Amazon S3 Bucket ]
                                                         │
                                                         ▼
                                            [ Live Public Website ]

🚀 Key Features
Automated CI/CD: Continuous Deployment triggered on every code push to the main branch.

Granular IAM Security: Principle of Least Privilege enforcement using dedicated IAM policy actions (s3:PutObject, s3:GetObject, s3:DeleteObject).

Optimized Syncing: Efficient deployment using aws s3 sync to upload only changed assets while excluding metadata files (.git/*).

Cost Guardrails: Integrated zero-spend budget tracking via AWS Budgets to prevent unexpected billing.

🛠️ Technologies Used
Cloud Platform: Amazon Web Services (AWS S3, IAM, AWS Budgets)

CI/CD Tooling: GitHub Actions

Version Control: Git & GitHub

Frontend: HTML5, CSS3

⚙️ CI/CD Workflow (.github/workflows/deploy.yml)
YAML
name: Deploy Website to AWS S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Sync Files to S3
        run: |
          aws s3 sync . s3://shantanu-cloud-project-2026 --delete --exclude ".git/*"


👤 Author
Shantanu Lande

GitHub: @Shantanu-lande

Domain Focus: Cloud Support, DevOps & Cloud Engineering