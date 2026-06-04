pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                sh '''
                docker run --rm \
                -v $PWD:/workspace \
                -w /workspace \
                maven:3.9.6-eclipse-temurin-17 \
                mvn clean test
                '''
            }
        }
    }

    post {
        always {
            junit testResults: '**/target/surefire-reports/*.xml',
                  allowEmptyResults: true

            archiveArtifacts artifacts: '**/target/*.jar',
                             allowEmptyArchive: true
        }
    }
}
