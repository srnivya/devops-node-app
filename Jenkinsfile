pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = 'dockerhub-creds'   // Jenkins Credentiials ID
        IMAGE_NAME = 'srnivya/devops-node-app'   // Docker Hub repo
        CONTAINER_NAME = 'devops-node-app'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/srnivya/devops-node-app.git',
                    credentialsId: 'github-pat'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${IMAGE_NAME}:latest .
                """
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS}", usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh """
                    echo "$PASS" | docker login -u "$USER" --password-stdin
                    docker push ${IMAGE_NAME}:latest
                    """
                }
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker rm -f ${CONTAINER_NAME} || true
                docker run -d -p 3000:3000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:latest
                """
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline Completed Successfully!"
        }
        failure {
            echo "❌ Pipeline Failed"
        }
    }
}
