pipeline {
    agent any

    stages {
        stage('Install Maven') {
          steps {
            sh 'apt install maven'
          }
        }

        stage('Build') {
            steps {
                sh 'mvn clean verify -DskipTests'
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

