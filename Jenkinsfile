 pipeline {
  agent any

  environment {
    DOCKERHUB = credentials('DockerHub')         // Exposes DOCKERHUB_USR / DOCKERHUB_PSW
    SERVICE = 'web'                              // <-- match this to your compose service name
    REPORT_IN_CONTAINER = '/var/www/html/tests/report.xml'
    REPORT_LOCAL = 'report.xml'
  }

  stages {
    stage('Docker Login') {
      steps {
        sh 'echo "$DOCKERHUB_PSW" | docker login -u "$DOCKERHUB_USR" --password-stdin'
      }
    }

    stage('Pull , build and Run dockerfile ') {
      steps {
       
      sh '''
                docker stop myapp6 || true
		        docker rm myapp6 || true
		        docker rmi bassam2080/myapp6 || true
		        docker build -t bassam2080/myapp6  . 
				docker compose up -d
        
        '''
      }
    }

   

    
    stage('Run Tests') {
      steps {
        echo "done testing"
      }
    }

  stage ('cleaning'){
  steps{sh  'docker compose down'
	sh 'docker compose down || true'
	   }
  }
  
}
 }
