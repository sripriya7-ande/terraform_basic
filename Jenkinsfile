pipeline {
    agent any // Runs on any available agent; specify a label if necessary
    tools {
        terraform 'terraform' // Ensure Terraform is configured under "Manage Jenkins > Global Tool Configuration"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', credentialsId: 'terraform-token', url: 'https://github.com/sripriya7-ande/terraform_basic.git'
            }
        }
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }
        stage('Terraform Apply') {
            steps {
                input message: 'Proceed with Terraform Apply?', ok: 'Apply'
                sh 'terraform approve tfplan'
            }
        }
        stage('Verify File Creation') {
            steps {
                sh 'ls -l $WORKSPACE/pets.txt || echo "File not found!"'
                sh 'cat $WORKSPACE/pets.txt || echo "No content!"'
            }
        }
    }
}
