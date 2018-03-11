pipeline {
    environment {
        DOCKER_REGISTRY_PASSWORD = credentials('docker-registry-password')
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
                sh 'cd backend && ./gradlew check'
            }
        }

        stage('Dockerize') {
            steps {
                sh "cd docker && ./gradlew publishImages -Ppwd=$DOCKER_REGISTRY_PASSWORD"
            }
        }

        stage('Deploy') {
            steps {
                sh 'cd docker && ./gradlew deploy'
            }
        }
    }
}