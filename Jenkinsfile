pipeline {
    triggers {
        githubPush()
    }
    agent any

    environment {
        APP_NAME    = "spring-petclinic"
        DOCKER_USER = "rizjosel"
        IMAGE_TAG   = "${BUILD_NUMBER}"
        IMAGE_NAME  = "${DOCKER_USER}/${APP_NAME}:${IMAGE_TAG}"
    }

    stages {

        stage('List Workspace') {
            steps {
                sh 'ls -l'
		sh 'ls'
            }
        }

        stage('Build Application (Maven)') {
            steps {
                sh './mvnw clean package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build image with Docker Hub–compatible name
                sh 'docker build -t ${IMAGE_NAME} .'

                // Optional: save image as artifact
                sh 'docker save -o ${APP_NAME}-${IMAGE_TAG}.tar ${IMAGE_NAME}'
                archiveArtifacts artifacts: "${APP_NAME}-${IMAGE_TAG}.tar", fingerprint: true
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push ${IMAGE_NAME}
                        docker logout
                    '''
                }
            }
        }
    }
}
