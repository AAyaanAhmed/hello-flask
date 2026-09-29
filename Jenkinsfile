pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'docker build -t hello-flask .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'kubectl apply -f k8s'
            }
        }
    }
}
