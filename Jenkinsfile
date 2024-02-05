pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                // Checkout code from Github repository
                script {
                    git branch: 'main', url: 'https://github.com/nupursharma26/DevOps-Pipeline-Project.git'
                }
            }
        }
        stage('UNIT Testing') {
            steps {
                // Run unit tests using Maven
                script {
                    sh '/path/to/maven/bin/mvn verify'
                }
            }
        }
        stage('Maven Build') {
            steps {
                // Run Maven clean install
                script {
                    sh '/path/to/maven/bin/mvn clean install'
                }
            }
        }
    }
}

        
