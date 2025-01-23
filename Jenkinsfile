pipeline {
    agent any

    environment {
        // Utilisez les credentials Docker Hub configurés dans Jenkins
        DOCKER_HUB_CREDENTIALS = credentials('salah3779777/jenkinse')
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Construire l'image Docker avec le nom et le tag appropriés
                    docker.build("salah3779777/my-devops-app:${env.BUILD_ID}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Pousser l'image Docker vers Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'DOCKER_HUB_CREDENTIALS') {
                        docker.image("salah3779777/my-devops-app:${env.BUILD_ID}").push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Déployer l'application sur Kubernetes
                    sh """
                        kubectl apply -f k8s-deployment.yaml
                        kubectl apply -f k8s-service.yaml
                    """
                }
            }
        }
    }
}
