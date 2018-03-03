pipeline {
    agent any
    stages {
        stage('Test Backend') {
            agent {
                docker { image 'chkeller:java-buildstack' }
            }
            steps {
                sh 'cd backend && ./gradlew test check'
            }
        }
        stage('Test Frontend') {
            steps {
                sh 'cd frontend && ./gradlew build'
            }
        }
        stage('Build Backend Image') {

        }
        stage('Publish images') {
            steps {
                sh 'cd docker/proxy && docker build --name proxy .'
                sh 'cd docker/frontend && docker build --name frontend .'
                sh 'cd docker/backend && docker build --name backend .'
            }
        }
        stage('Test docker composition') {
            steps {
                // sh 'cd docker && docker-compose up -d && sleep 20'
                // sh 'cd docker && docker-compose down'
            }
        }
        stage('Deploy test system') {

        }
        stage('Deploy production') {

        }
    }
}