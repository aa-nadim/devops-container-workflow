pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/aa-nadim/devops-container-workflow.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build --no-cache -t flask-app .'
            }
        }
        stage('Run Flask App') {
            steps {
                sh '''
                docker rm -f flask-app || true
                docker run -d -p 5000:5000 --name flask-app flask-app
                '''
            }
        }
    }
}

