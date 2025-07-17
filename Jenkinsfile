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
