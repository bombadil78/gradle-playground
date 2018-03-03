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
                sh 'cd frontend && ng build --prod'
                sh 'cd backend && ./gradlew build'
            }
        }
        stage('Dockerize') {
            steps {
                sh 'cd docker && ./gradlew copyBackend'
                sh 'cd docker && ./gradlew copyFrontend'
            }
        }
    }
}