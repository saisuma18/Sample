pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/saisuma18/Sample.git'
            }
        }

        stage('Build Docker Image Locally') {
            steps {
                sh 'docker build -t Sample .'
            }
        }

        stage('Deploy to Remote EC2') {
            steps {
                sshagent(['Jenkins1']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ec2-user@13.200.226.125 '
                        docker stop calculator || true &&
                        docker rm calculator || true &&
                        docker rmi Sample || true &&
                        cd /home/ec2-user &&
                        git clone https://github.com/saisuma18/Sample.git || true &&
                        cd Sample &&
                        docker build -t Sample . &&
                        docker run -d -p 8080:80 --name calculator Sample
                    '
                    '''
                }
            }
        }
    }
}
