pipeline {
    agent any
    stages {
        stage('Create Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name s3Bucket --template-body file://s3_template.json --region 'us-east-1'"
              }
             }
            }
            }
