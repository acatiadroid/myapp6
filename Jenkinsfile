pipeline {
  agent any

  environment {
    DOCKERHUB = credentials('DockerHub')         // Exposes DOCKERHUB_USR / DOCKERHUB_PSW
    DOCKER_HOST = 'tcp://docker:2376'
  }

  stages {
    stage('Docker Login') {
      steps {
        sh 'echo "$DOCKERHUB_PSW" | docker login -u "$DOCKERHUB_USR" --password-stdin'
      }
    }

    stage('Pull, Build, and Run Dockerfile') {
      steps {
        sh '''
          docker ps -q -f name=myapp6 && docker stop myapp6 || true
          docker ps -a -q -f name=myapp6 && docker rm myapp6 || true
          docker images -q acatia/myapp6 && docker rmi acatia/myapp6 || true
          docker build -t acatia/myapp6 .
          docker-compose up -d
        '''
      }
    }

    stage('Run Tests') {
      steps {
        echo "done testing"
      }
    }

    stage('Cleaning') {
      steps {
        sh 'docker-compose down || true'
      }
    }
  }
}
