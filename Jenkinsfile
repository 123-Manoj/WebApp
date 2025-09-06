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
                bat '"C:\\Program Files\\Apache\\Maven\\maven-mvnd-1.0.2-windows-amd64\\bin\\mvnd.cmd" clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t simple-webapp .'
            }
        }

        stage('Cleanup Old Container') {
            steps {
                bat '''
                for /f "tokens=*" %%i in ('docker ps -aq -f name=simple-webapp') do (
                    docker stop %%i
                    docker rm %%i
                )
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 9090:9090 --name simple-webapp simple-webapp'
            }
        }
    }
}
