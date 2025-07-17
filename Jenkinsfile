pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'akhil06portfolio-site'
    }

    stages {
        stage('Upload to S3') {
            steps {
                withAWS(credentials: 'aws-jenkins', region: "${AWS_DEFAULT_REGION}") {
                    s3Upload(bucket: "${S3_BUCKET}", workingDir: '.', includePathPattern: '**/*')
                }
            }
        }
    }
}
