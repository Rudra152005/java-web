pipline{
    agent{
        docker{
            image 'maven:3.9.6-eclipse-temurin-17'
        }
    }
    stages{
        stage('checkout'){
            steps{
                checkout scm
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean compile'
            }
        }
        stage ('Test'){
            steps{
                sh 'mvn test'
            }
        }
    }
    post{
        always{
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
    }
}