pipeline {
    agent any

    environment {
        IMAGE_NAME = "spring-petclinic"
        CONTAINER_NAME = "petclinic-container"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/varadsawantcodelab/spring-petclinic.git'
            }
        }

        stage('Build Docker Image (includes Maven build)') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p 8080:8080 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }
}
