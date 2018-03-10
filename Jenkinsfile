pipeline {
    environment {
        USERNAME = credentials('username')
        PASSWORD = credentials('password')
    }
    agent {
        docker {
            image 'chkeller/buildstack'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Test') {
            steps {
                sh 'echo $USERNAME'
                sh 'echo $PASSWORD'
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
        stage('Publish') {
            steps {
                sh 'echo \'Push to versioned images to registry\''
                sh 'echo \'Publish docker-compose as artifact\''
            }
        }
    }
}