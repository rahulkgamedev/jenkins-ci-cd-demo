pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t task2-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker images | grep task2-app'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f task2-container || true

                docker run -d \
                --name task2-container \
                -p 5000:5000 \
                task2-app
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
