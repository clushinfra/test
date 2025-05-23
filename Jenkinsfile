pipeline {
  agent any
  environment {
    IMAGE = "nexus.yourdomain.com/web/test-html:latest"
  }
  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/clushinfra/test.git'
      }
    }
    stage('Build Image') {
      steps {
        script {
          dockerImage = docker.build("${IMAGE}")
        }
      }
    }
    stage('Push to Nexus') {
      steps {
        script {
          docker.withRegistry('http://nexus.yourdomain.com', 'nexus-creds') {
            dockerImage.push()
          }
        }
      }
    }
  }
}
