pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build Docker Image') {
      steps { sh 'docker build -t myapp:latest .' }
    }
    stage('Deploy') {
      steps {
        sh 'docker stop myapp || true'
        sh 'docker rm myapp || true'
        sh 'docker run -d --name myapp -p 3000:3000 myapp:latest'
      }
    }
    stage('Health Check') {
      steps { sh 'sleep 3 && curl -f http://localhost:3000' }
    }
  }
}
