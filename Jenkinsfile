pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-demo-app"
        CONTAINER_NAME = "jenkins-demo-container"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/YOUR_USERNAME/jenkins-ci-cd-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker images | grep $IMAGE_NAME'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true

                docker run -d \
                --name $CONTAINER_NAME \
                -p 5000:5000 \
                $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
