pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_TAG  = "1.0.0"
        GIT_REPO   = "https://github.com/rajkumar-pulaputhur/solar-system.git"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: "${GIT_REPO}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                """
            }
        }

        stage('Verify Image') {
            steps {
                sh "docker images | grep ${IMAGE_NAME}"
            }
        }
        stage('run image') {
            steps {
                sh "docker run -d --network=node-net -p 3000:3000 ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }

    post {
        success {
            echo "✅ Docker image built: ${IMAGE_NAME}:${IMAGE_TAG}"
        }
        failure {
            echo "❌ Build failed"
        }
    }
}
