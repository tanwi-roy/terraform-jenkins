pipeline {
    agent any

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: true, description: 'Automatically run apply after generating plan?')
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Select the action to perform')
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION    = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/tanwi-roy/terraform-jenkins.git'
            }
        }
        stage('Terraform init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Plan') {
            steps {
                sh 'terraform plan'
            }
        }
        stage('Apply') {
            steps {
                sh 'terraform apply'
            }
        }


//         stage('Apply / Destroy') {
//             steps {
//                 script {
//                     if (params.action == 'apply') {
//
//                         sh 'terraform apply'
//                     } else if (params.action == 'destroy') {
//                         sh 'terraform destroy'
//                     } else {
//                         error "Invalid action selected. Please choose either 'apply' or 'destroy'."
//                     }
//                 }
//             }
//         }

    }
}