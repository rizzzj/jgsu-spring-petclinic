pipeline {
    agent any

    stages {
        stage('bash') {
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
    }
}
