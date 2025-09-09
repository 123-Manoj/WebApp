pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/123-Manoj/WebApp.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t simple-webapp .'
            }
        }

        stage('Cleanup Old Container') {
            steps {
                sh '''
                docker stop simple-webapp || true
                docker rm simple-webapp || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 9090:9090 --name simple-webapp simple-webapp'
            }
        }
    }
}
