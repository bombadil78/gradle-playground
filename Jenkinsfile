pipeline {
    environment {
        DOCKER_REGISTRY_PASSWORD = 'emad1331'
    }

    agent {
        docker {
            image 'chkeller/buildstack'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
            reuseNode true
        }
    }

    stages {
        stage('Commit') {
            steps {
                sh 'cd backend && ./gradlew build check'
                sh 'cd frontend && ./gradlew build'
            }

            post {
                always {
                    sh 'echo \'publish junit results\''
                }
            }
        }

        stage('Dockerize') {
            steps {
                sh 'cd docker && ./gradlew publishImages'
                sh 'cd docker && ./gradlew publishDockerCompose'
            }
        }

        stage('Deploy') {
            steps {
                sh 'cd docker && ./gradlew deploy'
            }
        }
    }
}