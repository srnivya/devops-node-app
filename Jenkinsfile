pipeline {
    agent any

    environment {
        IMAGE_NAME = "srnivya/devops-node-app"
        DOCKER_CREDENTIALS = "dockerhub-creds"
        GIT_CREDENTIALS = "github-pat"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    credentialsId: "${GIT_CREDENTIALS}",
                    url: 'https://github.com/srnivya/devops-node-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS}", usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh """
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE_NAME
                    """
                }
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop node-app || true
                docker rm node-app || true
                docker run -d -p 3000:3000 --name node-app $IMAGE_NAME
                '''
            }
        }
    }
}
