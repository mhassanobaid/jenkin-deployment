pipeline {
    agent any

    environment {
        IMAGE_NAME = '0.0.1.RELEASE'
        CONTAINER_NAME = 'jenkins-deployment'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mhassanobaid/jenkin-deployment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
                echo "Building Docker image..."
            }
        }

        stage('Run Docker Container') {
            steps {
                // Stop old container if running
                sh "docker rm -f ${CONTAINER_NAME} || true"

                // Run new container
                sh "docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${IMAGE_NAME}"
            }
        }
    }
}