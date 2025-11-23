Rita Portfolio Website — AWS S3 + GitHub Actions CI/CD
===============================================
 Project Overview
This project hosts and automates the deployment of my personal portfolio website using AWS S3 and GitHub Actions.
It demonstrates how continuous integration and deployment (CI/CD) can keep a static website up-to-date automatically — without manually uploading files to AWS.

 Project Architecture
work-done/
│
├── index.html
├── about.html
├── contact.html
├── assets/
│   ├── css/
│   ├── js/
│   ├── images/
│
└── .github/
    └── workflows/
        └── code.yml



HTML, CSS, JS — Website files


AWS S3 — Static website hosting


GitHub Actions — Automates deployment to S3 on every push



 Setup Steps:
1️⃣ Create GitHub Repository


Repository name: Rita-portfolio-website


Do not initialize with README or .gitignore


2️ Prepare Local Folder


Folder name: work-done


Inside it, paste all website files (index.html, CSS, JS, images)


Create .github/workflows/code.yml inside the same folder


3️⃣ Connect to GitHub
git init
git add .
git commit -m "Initial commit - Portfolio Website"
git branch -M main
git remote add origin https://github.com/yourusername/Rita-portfolio-website.git
git push -u origin main


 CI/CD Workflow (.github/workflows/code.yml)
name: Deploy Portfolio to AWS S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Upload Website to S3
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Sync files to S3 bucket
        run: |
          aws s3 sync . s3://your-s3-bucket-name --delete


Replace your-s3-bucket-name with your actual S3 bucket name.


 GitHub Secrets Configuration


Go to GitHub → Repo Settings → Secrets and Variables → Actions


Add the following:


AWS_ACCESS_KEY_ID


AWS_SECRET_ACCESS_KEY




These are obtained from your AWS IAM user.

 How the Automation Works (CI/CD Explained)
Once the workflow is configured:


You edit your index.html or any file (e.g., update content, add new sections).


Save your changes and push to GitHub:
git add .
git commit -m "Updated homepage content"
git push



GitHub Actions automatically triggers:


Fetches the latest code


Configures AWS credentials


Uploads updated files to your S3 bucket




 Within minutes, your S3 website reflects the new version automatically.

 Accessing the Website


Go to your AWS S3 console → Bucket → Properties → Static Website Hosting


Copy the Website endpoint URL


Open it in your browser to view your live portfolio site.


Example:
http://rita-portfolio-bucket.s3-website-us-east-1.amazonaws.com


 Future Improvements


Add CloudFront + SSL (HTTPS) for better performance and security


Enable versioning in S3


Add a custom domain name (via Route 53 or Namecheap)



 Author
RITA (Ritacloud23)
Cloud & DevOps Engineer | AWS | Terraform | Docker | CI/CD | Kubernetes
LinkedIn | GitHub | Portfolio

