pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh '''
                docker run --rm \
                  -v "$PWD":/app \
                  -w /app \
                  maven:3.9.6-eclipse-temurin-17 \
                  mvn clean verify -DskipTests
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t java-devops-demo:1.0 .'
            }
        }

        stage('Docker Compose') {
            steps {
                sh 'docker-compose up -d --build'
            }
        }

        stage('Health Check') {
            steps {
                sh 'curl -f http://localhost:8080'
            }
        }
    }

    post {
        success {
            echo '✅ CICD Pipeline successful'
        }
        failure {
            echo '❌ CICD Pipeline failed'
        }
    }
}

