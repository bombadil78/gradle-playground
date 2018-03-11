pipeline {
    agent {
        docker {
            image 'chkeller/buildstack'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Commit') {
            steps {
                sh 'cd backend && ./gradlew check'
            }
        }

        stage('Dockerize') {
            steps {
                sh 'cd docker && ./gradlew buildBackendImage'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo todo'
            }
        }
    }
}