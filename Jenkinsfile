pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-react-app:latest .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker stop my-react-container || true
                    docker rm my-react-container || true
                    docker run -d --name my-react-container -p 8080:80 my-react-app:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'React application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
