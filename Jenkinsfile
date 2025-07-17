pipeline {
  agent any

  environment {
    BUCKET_NAME = 'akhil06portfolio-site'
    REGION = 'us-east-1'
  }

  stages {
    stage('Deploy to S3') {
      steps {
        withAWS(credentials: 'aws-s3-creds', region: "${REGION}") {
          bat 'aws s3 sync . s3://%BUCKET_NAME% --delete'
        }
      }
    }
  }
}
