pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/rizzzj/jgsu-spring-petclinic.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t spring-petclinic:${BUILD_NUMBER} .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                  docker rm -f petclinic || true
                  docker run -d -p 8080:8080 --name petclinic spring-petclinic:${BUILD_NUMBER}
                '''
            }
        }
    }
}
