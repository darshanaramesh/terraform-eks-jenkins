pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-creds',
                    url: 'https://github.com/darshanaramesh/terraform-eks-jenkins.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh 'trivy config .'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }

        stage('Terraform Apply') {
            input {
                message "Create / Update EKS?"
                ok "Apply"
            }
            steps {
                sh 'terraform apply -auto-approve'
            }
        }

        stage('Terraform Destroy') {
            input {
                message "Destroy EKS?"
                ok "Destroy"
            }
            steps {
                sh 'terraform destroy -auto-approve'
            }
        }
    }
}

