pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/user/springboot-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        success {
            echo 'Pipeline CI/CD exécuté avec succès '
        }
        failure {
            echo 'Erreur dans le pipeline '
        }
    }
}
