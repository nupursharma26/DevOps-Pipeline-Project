pipeline {
    agent any

    environment {
        // Reference the GitHub credentials by ID
        GITHUB_CREDENTIALS = credentials('pipeline') // Line 4
    }

    stages {
        stage('Git Checkout') {
            steps {
                // Checkout code from GitHub repository
                git branch: 'main', credentialsId: env.GITHUB_CREDENTIALS, url: 'https://github.com/nupursharma26/DevOps-Pipeline-Project.git' // Line 10
            }
        }
        stage('UNIT Testing') {
            steps {
                // Run unit tests using Maven
                sh '"/opt/homebrew/bin/mvn" verify' // Line 16
            }
        }
        stage('Maven Build') {
            steps {
                // Run Maven clean install
                sh '"/opt/homebrew/bin/mvn" clean install' // Line 22
            }
        }
        stage('Deploy with Ansible') {
            steps {
                // Execute Ansible playbook
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }
    }
}
