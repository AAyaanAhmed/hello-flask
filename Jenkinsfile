pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ayaanahmad2003/hello-flask:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push ayaanahmad2003/hello-flask:latest'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@65.1.93.162 "
                    docker pull ayaanahmad2003/hello-flask:latest &&
                    docker stop hello-flask || true &&
                    docker rm hello-flask || true &&
                    docker run -d -p 5000:5000 --name hello-flask ayaan123/hello-flask:latest
                    "
                    '''
                }
            }
        }
    }
}