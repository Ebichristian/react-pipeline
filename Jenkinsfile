
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
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
                sh 'docker build -t react-pipeline:v1 .'
            }
        }
        stage('Push Docker Image') {
    	    steps {
              withCredentials([usernamePassword(
            	credentialsId: 'dockerhub-creds',
            	usernameVariable: 'DOCKER_USERNAME',
            	passwordVariable: 'DOCKER_PASSWORD'
        	)]) {
            	sh '''
                	echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                	docker tag react-pipeline:v1 $DOCKER_USERNAME/react-pipeline:v1
                	docker push $DOCKER_USERNAME/react-pipeline:v1
           	   '''
       			 }
    		}	
	}

    }
}

