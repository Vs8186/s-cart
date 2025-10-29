pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred')  // Add in Jenkins Credentials
        DOCKER_IMAGE = "veena1909/s-cart"
        K8S_DEPLOYMENT_BLUE = "s-cart-blue"
        K8S_DEPLOYMENT_GREEN = "s-cart-green"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/Vs8186/s-cart.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE:$BUILD_NUMBER .'
                }
            }
        }

        stage('Push Docker Image to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                        sh 'docker push $DOCKER_IMAGE:$BUILD_NUMBER'
                    }
                }
            }
        }

        stage('Blue-Green Deployment on Kubernetes') {
            steps {
                script {
                    def currentColor = sh(script: "kubectl get svc s-cart-service -o=jsonpath='{.spec.selector.color}'", returnStdout: true).trim()
                    def newColor = (currentColor == 'blue') ? 'green' : 'blue'

                    sh """
                    kubectl set image deployment/s-cart-$newColor s-cart=$DOCKER_IMAGE:$BUILD_NUMBER --record
                    kubectl rollout status deployment/s-cart-$newColor
                    kubectl patch service s-cart-service -p '{\"spec\":{\"selector\":{\"app\":\"s-cart\",\"color\":\"$newColor\"}}}'
                    """
                }
            }
        }
    }
}
