pipeline {
  agent { label 'app' }   // Se ejecuta en el agente remoto (app)
  environment {
    IMAGE = "labwebapp:latest"
    CONTAINER = "webapp"
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Docker Image') {
      steps {
        sh "docker build -t ${IMAGE} ."
      }
    }
    stage('Stop old container') {
      steps {
        sh "docker rm -f ${CONTAINER} || true"
      }
    }
    stage('Run new container') {
      steps {
        sh "docker run -d --name ${CONTAINER} -p 8080:80 ${IMAGE}"
      }
    }
  }
  post {
    success {
      echo "Despliegue completado en app (${IMAGE})"
    }
  }
}
