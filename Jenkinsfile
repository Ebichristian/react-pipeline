pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ebichristian/react-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-react-app:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker stop my-react-app || true
                    docker rm my-react-app || true
                    docker run -d --name my-react-app -p 3000:80 my-react-app:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'React app deployed successfully!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}
