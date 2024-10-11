pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'hello-world-app:latest'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/<ton-utilisateur>/hello-world-app.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh "kubectl apply -f deployment.yaml"
                    sh "kubectl apply -f service.yaml"
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
