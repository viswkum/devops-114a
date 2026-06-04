pipeline {
    agent any

    environment {
        REPO_URL = "https://github.com/viswkum/hellow-wrld.git"
        IMAGE_NAME = "hello-world-app"
        TAG = "v1"
        CONTAINER_NAME = "hello-container"
        PORT = "8090"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'master', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME:$TAG ."
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker rm -f $CONTAINER_NAME || true
                docker run -d -p $PORT:8080 --name $CONTAINER_NAME $IMAGE_NAME:$TAG
                """
            }
        }

        stage('Verify') {
            steps {
                sh "docker ps"
            }
        }
    }
}
