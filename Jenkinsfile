pipeline {
    agent any

    
    stages {
        stage('Git Checkout') {
            steps {
                // Checkout code from Github repository
               git branch: 'main', url: 'https://github.com/preet0807/DevOps.git'
            }
        }
        stage ('UNIT testing'){
            steps{
                bat '/C:/Program Files/apache-maven-3.9.1-bin/apache-maven-3.9.1/mvn verify -DskipUnitTests'
            }
        
        }
        stage('Maven Build'){
            steps{
                bat '/C:/Program Files/apache-maven-3.9.1-bin/apache-maven-3.9.1/mvn clean install '
            }
        }
    }
}


        
