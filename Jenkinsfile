pipeline {
    agent any
    environment {
        APP_NAME = "spring-petclinic"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('List Workspace') {
            steps {
                sh 'ls'
                sh 'ls -l'
            }
        }

        stage('Build Application (Maven)') {
            steps {
                sh './mvnw clean package -DskipTests'
                sh 'ls'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${APP_NAME}:${IMAGE_TAG} .'
                sh 'ls'
            }
        }
    }
}
