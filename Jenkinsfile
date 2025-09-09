pipeline {
    agent any

    tools {
        maven 'Maven_3.8.4'   // name from Global Tool Configuration
        jdk 'Java_21'       // name from Global Tool Configuration
    }

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
                # Stop and remove existing container if it exists
                if [ $(docker ps -aq -f name=simple-webapp) ]; then
                    docker stop simple-webapp || true
                    docker rm simple-webapp || true
                fi
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
