pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t 176039391845.dkr.ecr.us-east-2.amazonaws.com/web-app:1.0.2 .'
            }
        }

        stage('Login to ECR') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Demo-coolweb', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh 'eval $(aws ecr get-login --no-include-email --region us-east-2)'
                }
            }
        }

        stage('Push to ECR') {
            steps {
                sh 'docker push 176039391845.dkr.ecr.us-east-2.amazonaws.com/web-app:1.0.2'
            }
        }

        stage('Logout from ECR') {
            steps {
                sh 'docker logout 176039391845.dkr.ecr.us-east-2.amazonaws.com'
            }
        }
    }
}