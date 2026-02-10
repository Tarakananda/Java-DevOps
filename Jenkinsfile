pipeline {
    agent any
    
    environment{
       IMAGE_NAME = "java_image"
       IMAGE_TAG = "1.0"
     }
    stages {
      stage('Checkout Code') {
        steps {
          git branch: 'main', url: 'https://github.com/Tarakananda/Java-DevOps.git'
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

