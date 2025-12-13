pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/rizzzj/jgsu-spring-petclinic.git'
            }
        }

        stage('bash') {
            steps {
                sh 'ls'
                sh 'ls -l'
            }
        }
    }
}
