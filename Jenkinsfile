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

            post {
                always {
                    junit 'backend/build/reports/**/*.html'
                }
            }
        }
    }
}