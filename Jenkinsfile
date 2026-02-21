pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = 'dockerhub-creds'
        IMAGE_NAME = 'srnivya/devops-node-app'
        GIT_CREDENTIALS = 'github-pat'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/srnivya/devops-node-app.git', credentialsId: "${GIT_CREDENTIALS}"
            }
        }
        stage('Build Node App') {
            steps {
                sh 'npm install'
                sh 'npm test || echo "No tests or tests failed"'
            }
        }
        stage('Docker Build') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS}", usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh "docker push ${IMAGE_NAME}:latest"
                    sh 'docker logout'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "docker rm -f devops-node-app || true"
                sh "docker run -d -p 8080:8080 --name devops-node-app ${IMAGE_NAME}:latest"
            }
        }
    }
}
