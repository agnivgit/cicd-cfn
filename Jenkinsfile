pipeline {
    agent any
    stages {
        stage('Create Stack into Dev Env') {
            steps {
            sh '''
                set +x
                unset AWS_ACCESS_KEY_ID
                unset AWS_SECRET_ACCESS_KEY
                unset AWS_SESSION_TOKEN
                creds_json=$(aws sts assume-role  --role-arn  $DEV_ROLE_ARN --role-session-name devSession --region us-east-1)
                export AWS_ACCESS_KEY_ID=$(echo "$creds_json" | jq .Credentials.AccessKeyId |tr -d '"')
                export AWS_SECRET_ACCESS_KEY=$(echo "$creds_json" | jq .Credentials.SecretAccessKey| tr -d '"')
                export AWS_SESSION_TOKEN=$(echo "$creds_json" | jq .Credentials.SessionToken|tr -d '"')
                set -x
                aws cloudformation create-stack --stack-name s3bucket --template-body file://s3_template.json --region us-east-1
                '''
              }
            }    
        stage('Create Stack into Prod Env'){
            input{
                message "Do you want to proceed for production deployment?"
            }    
            steps {
            sh '''
                set +x
                unset AWS_ACCESS_KEY_ID
                unset AWS_SECRET_ACCESS_KEY
                unset AWS_SESSION_TOKEN
                creds_json=$(aws sts assume-role  --role-arn  $PROD_ROLE_ARN --role-session-name devSession --region us-east-1)
                export AWS_ACCESS_KEY_ID=$(echo "$creds_json" | jq .Credentials.AccessKeyId |tr -d '"')
                export AWS_SECRET_ACCESS_KEY=$(echo "$creds_json" | jq .Credentials.SecretAccessKey| tr -d '"')
                export AWS_SESSION_TOKEN=$(echo "$creds_json" | jq .Credentials.SessionToken|tr -d '"')
                set -x
                aws cloudformation create-stack --stack-name s3bucket --template-body file://s3_template.json --region us-east-1
                '''
              }
            }
        }    
    }
