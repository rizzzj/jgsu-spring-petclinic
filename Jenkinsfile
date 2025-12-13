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
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                sh 'ls'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${APP_NAME}:${IMAGE_TAG} .'
                sh "docker save -o ${APP_NAME}-${IMAGE_TAG}.tar ${APP_NAME}:${IMAGE_TAG}"
                archiveArtifacts artifacts: "${APP_NAME}-${IMAGE_TAG}.tar", fingerprint: true
            }
        }
    }
}
