 pipeline {
  agent any //test

  environment {
    DOCKERHUB = credentials('DockerHub')         // Exposes DOCKERHUB_USR / DOCKERHUB_PSW
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
		        docker rmi acatia/myapp6 || true
		        docker build -t acatia/myapp6  . 
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
  steps{
	  sh  'docker compose down'
	sh 'docker compose down || true'
	   }
  }
  
}
 }
