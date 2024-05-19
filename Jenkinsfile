pipeline {
    agent any

    environment {
        // Reference the GitHub credentials by ID
        GITHUB_CREDENTIALS = credentials('gitcred')
    }

    stages {
        stage('Git Checkout') {
            steps {
                // Checkout code from GitHub repository
                git branch: 'main', credentialsId: gitcred, url: 'https://github.com/nupursharma26/DevOps-Pipeline-Project.git'
            }
        }
        stage('UNIT Testing') {
            steps {
                // Run unit tests using Maven
                sh script: '"/opt/homebrew/bin/mvn" verify -DskipUnitTests', returnStatus: true
            }
        }
        stage('Maven Build') {
            steps {
                // Run Maven clean install
                sh '"/opt/homebrew/bin/mvn" clean install'
            }
        }
    }
}


        
