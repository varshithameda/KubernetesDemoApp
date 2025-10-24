pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image"
                bat 'docker build -t kubdemoapp:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                bat 'docker login -u srivarshithameda -p '
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                echo "Pushing Docker Image to Docker Hub"
                bat 'docker tag kubdemoapp:v1 srivarshithameda/sample:kubelmager'
                bat 'docker push srivarshithameda/sample:kubelmager'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying to Kubernetes"
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}