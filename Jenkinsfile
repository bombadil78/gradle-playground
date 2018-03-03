pipeline {
    agent {
        docker {
            image 'chkeller/buildstack'
        }
    }
    stages {
        stage('Test') {
            steps {
                sh 'cd backend && ./gradlew test check'
            }
        }
        stage('Build') {
            steps {
                sh 'cd frontend && ./gradlew build'
                sh 'cd backend && ./gradlew build'
            }
        }
        stage('Dockerize') {
            steps {
                sh 'cd docker && ./gradlew buildBackendImage'
                sh 'cd docker && ./gradlew buildFrontendImage'
            }
        }
    }
}