pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-configure')  // ID from Jenkins credentials store
        AWS_SECRET_ACCESS_KEY = credentials('aws-configure')  // ID from Jenkins credentials store
     }

    stages {
        

        stage('Checkout') {
            steps {
                deleteDir()
                sh 'echo cloning repo'
                sh 'git clone https://github.com/Naresh-luffy/jenkins-terraform-ansible-task-challenge.git' 
            }
        }
        
        stage('Terraform Apply') {
            steps {
                script {
                    dir('/var/lib/jenkins/workspace/zoro1/jenkins-terraform-ansible-task-challenge/') {
                    sh 'pwd'
                    sh 'terraform init'
                   // sh 'terraform plan'
                     sh 'terraform destroy -auto-approve'
                    
                    sh 'terraform apply -auto-approve'
                    }
                }
            }
        }
        
        stage('Ansible Deployment') {
            steps {
                script {
                   sleep '360'
                    ansiblePlaybook becomeUser: 'ec2-user', credentialsId: 'amazon-linux', disableHostKeyChecking: true, installation: 'ansible', inventory: '/var/lib/jenkins/workspace/zoro1/jenkins-terraform-ansible-task-challenge/inventory.yaml', playbook: '/var/lib/jenkins/workspace/zoro1/jenkins-terraform-ansible-task-challenge/amazon-playbook.yml', vaultTmpPath: ''
                    ansiblePlaybook becomeUser: 'ubuntu', credentialsId: 'ubuntu', disableHostKeyChecking: true, installation: 'ansible', inventory: '/var/lib/jenkins/workspace/zoro1/jenkins-terraform-ansible-task-challenge/inventory.yaml', playbook: '/var/lib/jenkins/workspace/zoro1/jenkins-terraform-ansible-task-challenge/ubuntu-playbook.yml', vaultTmpPath: ''
                }
            }
        }
    }
}
