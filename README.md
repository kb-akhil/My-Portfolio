Portfolio Website - CI/CD Deployment (Jenkins + AWS S3)

This project showcases a CI/CD pipeline using **Jenkins** to automatically deploy a personal portfolio website to **AWS S3**.

Tech Stack
Frontend: HTML, CSS, JS
CI/CD: Jenkins
Cloud: AWS S3 (Static website hosting)

Prerequisites

1. AWS Account with:
   - An S3 Bucket (with static website hosting enabled).
   - An IAM user with programmatic access and S3 permissions.

2. Jenkins Installed:
   - Locally or on an EC2 instance.
   - Installed AWS CLI in Jenkins environment.
   - AWS credentials added to Jenkins using **Manage Credentials**.

3. GitHub Repository:
   - Your portfolio code should be in a GitHub repo.
   - `Jenkinsfile` must be present in the root.

Jenkins Credentials Setup

Create two **Secret Text** credentials in Jenkins:

| ID                  | Description           |
| ------------------- | --------------------- |
| `aws-s3-access-key` | AWS Access Key ID     |
| `aws-s3-secret-key` | AWS Secret Access Key |

> Go to **Jenkins → Manage Jenkins → Credentials → (Global)** and add them.

📜 Jenkinsfile
pipeline {
  agent any

  environment {
    AWS_ACCESS_KEY_ID     = credentials('aws-s3-access-key')
    AWS_SECRET_ACCESS_KEY = credentials('aws-s3-secret-key')
    BUCKET_NAME           = 'akhil06portfolio-site'
    REGION                = 'us-east-1'
  }

  stages {
    stage('Sync to S3') {
      steps {
        sh '''
          aws s3 sync . s3://$BUCKET_NAME --region $REGION --delete
        '''
      }
    }
  }
}

Deployment Steps
Clone the repo and make changes locally.

Push updates to GitHub.

Open Jenkins → Your Job → Click Build Now.

Your S3 bucket will get updated automatically.

 S3 Bucket Static Website URL
After deployment, visit:

php-template
Copy code
http://<your-bucket-name>.s3-website-<region>.amazonaws.com/

process video:https://drive.google.com/file/d/1xQL3v62R29TGCvRDtbNCrKgotp2Dola7/view?usp=sharing
