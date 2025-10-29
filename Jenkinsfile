pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred')
        IMAGE_NAME = "veena1909/s-cart"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Vs8186/s-cart.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat """
                docker build -t %IMAGE_NAME%:latest .
                """
            }
        }

        stage('Push Docker Image to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                    docker push %IMAGE_NAME%:latest
                    """
                }
            }
        }

        stage('Blue-Green Deployment on Kubernetes') {
            steps {
                bat """
                kubectl apply -f k8s/service.yaml
                kubectl apply -f k8s/deployment-blue.yaml
                """
            }
        }
    }
}
