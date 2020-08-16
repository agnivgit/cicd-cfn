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
                aws_credentials_json=$(aws sts assume-role --role-arn "${DEV_ROLE_ARN}" --role-session-name devSession --region 'us-east-1')
                export AWS_ACCESS_KEY_ID=$(echo “$aws_credentials_json” | jq — exit-status — raw-output .Credentials.AccessKeyId)
                export AWS_SECRET_ACCESS_KEY=$(echo “$aws_credentials_json” | jq — exit-status — raw-output .Credentials.SecretAccessKey)
                export AWS_SESSION_TOKEN=$(echo “$aws_credentials_json” | jq — exit-status — raw-output .Credentials.SessionToken)
                set -x
                aws cloudformation create-stack --stack-name s3bucket --template-body file://s3_template.json --region 'us-east-1'
                '''
              }
             }
            }
            }
