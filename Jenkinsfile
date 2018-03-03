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
        stage('Dockerize & push') {
            steps {
                sh 'cd docker && ./gradlew copyBackend'
                sh 'cd docker && ./gradlew copyFrontend'
                sh 'cd docker && docker build --tag chkeller/gradle-playground-proxy proxy'
                sh 'cd docker && docker build --tag chkeller/gradle-playground-backend backend'
                sh 'cd docker && docker build --tag chkeller/gradle-playground-backend frontend'
                sh 'echo \'push to repo here\''
            }
        }
    }
}