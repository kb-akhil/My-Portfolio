pipeline {
  agent any

  environment {
    BUCKET_NAME = 'akhil06portfolio-site'
    REGION = 'us-east-1'
  }

  stages {
    stage('Sync to S3') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-s3-secret-key']]) {
          sh '''
            aws s3 sync . s3://$BUCKET_NAME --region $REGION --delete
          '''
        }
      }
    }
  }
}
