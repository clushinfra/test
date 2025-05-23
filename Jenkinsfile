pipeline {
  agent any
  environment {
    IMAGE = "http://27.96.145.28:30081/web/test-html:latest"
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
          docker.withRegistry('http://27.96.145.28:30081/', 'admin') {
            dockerImage.push()
          }
        }
      }
    }
  }
}
