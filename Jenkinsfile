pipeline {
    agent any

    tools {
        jdk 'Java_21'   // 👈 This matches the JDK name in Jenkins settings
        maven 'Maven_3' // 👈 If you’ve also added Maven in Jenkins Tools
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/123-Manoj/WebApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Run') {
            steps {
                sh 'java -jar target/*.jar'
            }
        }
    }
}
