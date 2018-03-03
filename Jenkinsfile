pipeline {
    agent {
        docker {
            image 'gradle:4.6.0-jdk8-alpine'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'cd master && ./gradlew hello'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}