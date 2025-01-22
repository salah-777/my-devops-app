pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('salah3779777/jenkinse')
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("salah3779777/my-devops-app:${env.BUILD_ID}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("salah3779777/my-devops-app:${env.BUILD_ID}").push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh """
                        kubectl apply -f k8s-deployment.yaml
                        kubectl apply -f k8s-service.yaml
                    """
                }
            }
        }
    }
}
