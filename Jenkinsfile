pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-deployment:0.0.1.RELEASE'
        CONTAINER_NAME = 'flask-app'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
                echo "Building Docker image..."
            }
        }

        stage('Run Docker Container') {
            steps {
                // Stop old container if running
                echo "Running Docker container..."
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm -f ${CONTAINER_NAME} || true"

                // Run new container
                sh "docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                
            }
        }
    }
}

