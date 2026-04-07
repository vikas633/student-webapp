pipeline {
    agent any

    stages {
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t student-webapp:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop student-webapp || true
                docker rm student-webapp || true
                docker run -d -p 9090:8080 --name student-webapp student-webapp:${BUILD_NUMBER}
                '''
            }
        }
    }
}
