pipeline {
  agent any
  
  environment {
    DOCKERHUB_CREDENTIALS = credentials('rbonchev-dockerhub')
  }
  
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t rbonchev/java-web-app:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sh docker login -u $DOCKERHUB_CREDENTIALS_USR -password-stdin'
      }
    }
    stage('Push to Dockerhub') {
      steps {
        sh 'docker tag my-app-image rbonchev/java-web-app:latest'
        sh 'docker push rbonchev/java-web-app:latest'
      }
    }
    
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}