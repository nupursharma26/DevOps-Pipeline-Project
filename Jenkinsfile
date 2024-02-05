pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                // Checkout code from GitHub repository
                git branch: 'main', url: 'https://github.com/nupursharma26/DevOps-Pipeline-Project.git'
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


        
