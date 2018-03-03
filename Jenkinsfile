pipeline {
    agent none
    stages {
        stage('Test') {
            agent {
                docker {
                    image 'chkeller/java-buildstack'
                }
            }
            steps {
                sh 'cd backend && ./gradlew test check'
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'chkeller/java-buildstack'
                }
            }
            steps {
                sh 'cd backend && ./gradlew build'
                sh 'cd frontend && ./gradlew build'
            }
        }
        stage('Publish images') {
            steps {
                sh 'cd docker/proxy && docker build --name proxy .'
                sh 'cd docker/frontend && docker build --name frontend .'
                sh 'cd docker/backend && docker build --name backend .'
            }
        }
    }
}