pipeline {
    agent any

    environment {
        // Utilisez les credentials Docker Hub configurés dans Jenkins
        DOCKER_HUB_CREDENTIALS = credentials('jenkinse777')
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
                    // Remplacer ${BUILD_ID} dans le fichier YAML
                    sh """
                        export BUILD_ID=${env.BUILD_ID}
                        envsubst < k8s-deployment.yaml > k8s-deployment-substituted.yaml
                        kubectl apply -f k8s-deployment-substituted.yaml
                        kubectl apply -f k8s-service.yaml
                    """
                }
            }
        }
    }
}
