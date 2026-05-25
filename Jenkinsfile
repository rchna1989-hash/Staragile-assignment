pipeline {
    agent any
	tools {
        maven 'Maven3'
    }

    environment {
        IMAGE_NAME = 'staragile-app'
        CONTAINER_NAME = 'staragile-container'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/rchna1989-hash/Staragile-assignment.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'

                    sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:8080 --name myapp-container $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }
}