pipeline {
    agent any

    environment {
        // Reference the GitHub credentials by ID
        GITHUB_CREDENTIALS = credentials('pipeline') // Line 4
        NEXUS_CREDENTIALS = credentials('nexus-credentials')
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

         stage('SonarQube Analysis') {
            environment {
                SCANNER_HOME = tool name: 'Sonarserver', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            }
            steps {
                script {
                    def scannerHome = tool name: 'Sonarserver', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withEnv(["PATH+SCANNER=${scannerHome}/bin"]) {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=admin \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://192.168.1.2:9000/ \
                        -Dsonar.login=sqp_d34e025d6bc8e3285d1c27f8218f0a55fb8621e8
                        """
                    }
                }
            }
        }

        stage('Nexus Deployment') {
            steps {
        nexusArtifactUploader artifacts: [[
            artifactId: 'demo',
            classifier: '',
            file: 'target/demo-1.0-SNAPSHOT.jar',
            type: 'jar'
        ]], credentialsId: 'nexus-credentials', 
            groupId: 'com.example', 
            nexusUrl: 'localhost:8081', 
            protocol: 'http',
            nexusVersion: 'nexus3', 
            repository: 'maven-releases', 
            version: '1.0-SNAPSHOT'
           }
        }
        
    }
}
