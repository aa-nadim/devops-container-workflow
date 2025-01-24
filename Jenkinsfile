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
                sh 'docker build -t flask-app .'
            }
        }
        stage('Run Application') {
            steps {
                sh 'docker run -d -p 5000:5000 flask-app'
            }
        }
    }
}
