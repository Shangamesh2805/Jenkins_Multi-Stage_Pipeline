pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Shangamesh2805/Terraform_Jenkins_Multi_Pipeline.git', 
                    branch: env.gitlabSourceBranch, 
                  
            }
        }
        stage('Check Terraform Installation') {
            steps {
                ansiColor('xterm') {
                    echo 'Checking Terraform installation...'
                    sh 'terraform --version'
                }
            }
        }
        stage('Terraform Init') {
            steps {
                ansiColor('xterm') {
                    echo 'Initializing Terraform...'
                    sh 'terraform init'
                }
            }
        }
        stage('Terraform Plan') {
            steps {
                ansiColor('xterm') {
                    echo 'Setting up Terraform plan...'
                    sh 'terraform plan'
                }
            }
        }
        stage('Approval') {
            when {
                expression { env.gitlabSourceBranch == 'main' }
            }
            agent none
            steps {
                timeout(time: 15, unit: "MINUTES") {
                    input message: 'Do you want to approve the deployment?', ok: 'Yes'
                }
            }
        }
        stage('Terraform Apply') {
            when {
                expression { env.gitlabSourceBranch == 'main' }
            }
            steps {
                ansiColor('xterm') {
                    echo 'Terraform apply stage...'
                    sh 'terraform apply -auto-approve'
                }
            }
        }
    }
}
