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

        
        stage('SonarQube') {
            environment {
                SCANNER_HOME = tool 'SonarQube_Scanner'
            }
            steps {
                script {
                    def scannerHome = tool 'SonarQube Analysis'
                    withEnv(["PATH+SCANNER=${scannerHome}\\bin"]) {
                        bat 'sonar-scanner.bat \
                             -Dsonar.projectKey=admin \
                             -Dsonar.sources=. \
                             -Dsonar.host.url=http://192.168.1.6:9000/ \
                             -Dsonar.login=sqp_d34e025d6bc8e3285d1c27f8218f0a55fb8621e8'
                    }
                }
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_HOST_URL = 'http://localhost:9000'  // Default SonarQube URL
            }
            steps {
                withSonarQubeEnv('SonarQube') {  // 'SonarQube' should match the name of your SonarQube server configuration in Jenkins
                    sh '/opt/homebrew/bin/sonarqube sonar:sonar -Dsonar.projectKey=sqp_d34e025d6bc8e3285d1c27f8218f0a55fb8621e8 -Dsonar.host.url=http://192.168.1.6:9000/  -Dsonar.login=admin'
                }
            }
        }
        

        
    }
}
