pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credss')
        IMAGE_NAME = "adarsh347/jenkins-demo"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t ${IMAGE_NAME}:latest .
                '''
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh '''
                    echo "$DOCKERHUB_CREDENTIALS_PSW" | docker login \
                        -u "$DOCKERHUB_CREDENTIALS_USR" \
                        --password-stdin
                '''
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh '''
                    docker push ${IMAGE_NAME}:latest
                '''
            }
        }

        stage('Logout from Docker Hub') {
            steps {
                sh '''
                    docker logout
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
