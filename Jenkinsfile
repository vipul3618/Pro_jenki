pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-httpd-app"
        CONTAINER_NAME = "jenkins-httpd-container"
        PORT = "8081"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/YOUR_USERNAME/jenkins-httpd-deploy.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop & Remove Existing Container') {
            steps {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
            }
        }

        stage('Run New Container') {
            steps {
                sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:80 ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo "✅ Deployed: http://<your-server-ip>:${PORT}"
        }
        failure {
            echo "❌ Build failed."
        }
    }
}
