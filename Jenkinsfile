
pipeline {
  agent any

  stages {

    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t ahamid671/springboot-demo:latest .'
      }
    }

    stage('Push Docker Image') {
      steps {
        sh 'docker push ahamid671/springboot-demo:latest'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh '''
          kubectl apply -f kubernetes/deployment.yaml
          kubectl apply -f kubernetes/service.yaml
        '''
      }
    }
  }
}