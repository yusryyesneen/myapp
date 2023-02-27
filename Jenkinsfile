pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh('npm cache clean')
                sh ('npm install')
                sh ('npm run build')
            }
        }

        stage('Deploy') {
            environment {
                AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
                AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
            }
            steps {
                //withAWS(region: 'us-east-1', s3: 'newbucketweb') {
                    //sh 'aws s3 sync build/ s3://newbucketweb --delete'
                    sh "aws s3 cp */index.html s3://newbucketweb"
                }
            }
        }
    }

