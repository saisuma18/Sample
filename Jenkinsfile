pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/saisuma18/Sample.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("Sample")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop any old container
                    sh "docker stop calculator || true"
                    sh "docker rm calculator || true"
                    // Run new container
                    dockerImage.run("-d -p 8080:80 --name calculator")
                }
            }
        }
    }
}
