pipeline {
  agent any

  stages {

    stage('checkout') {
      steps {
        git ''
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean verify -DskipTests'
      }
    }

    stage('Dockerfile') {
      steps {
        sh 'docker build -t Java_image:1.0'
      }
    }

    stage('Docker-compose') {
      steps {
        sh '''
        docker compose down || true
        docker compose up
        '''
      }
    }

    stage('Health_check') {
      steps {
        sh '''
        sleep 15
        curl -f http://localhost:8081/actuator/health
        '''
      }
    }

    post {
      SUCCESS {
        echo 'CICD pipeline SUCCESSFULL"
      }
      FAILURE {
        echo 'CICD Pipeline failed'
      }
    }
  }
