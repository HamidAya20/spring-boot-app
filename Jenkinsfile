pipeline {
    agent any

    environment {
        IMAGE_NAME = "springboot-demo"
        HOST_PORT = "8081"
        CONTAINER_PORT = "8081"
    }

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker stop %IMAGE_NAME% || exit 0'
                bat 'docker rm %IMAGE_NAME% || exit 0'
                bat 'docker run -d -p %HOST_PORT%:%CONTAINER_PORT% --name %IMAGE_NAME% %IMAGE_NAME%'
            }
        }
    }
}
