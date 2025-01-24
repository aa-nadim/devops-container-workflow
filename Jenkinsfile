pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'flask-app'
        CONTAINER_NAME = 'flask-app'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aa-nadim/devops-container-workflow.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE} .'
            }
        }
        
        stage('Stop Existing Container') {
            steps {
                script {
                    sh """
                        docker stop ${CONTAINER_NAME} || true
                        docker rm ${CONTAINER_NAME} || true
                    """
                }
            }
        }
        
        stage('Run Flask App') {
            steps {
                sh """
                    docker run -d \
                    -p 5000:5000 \
                    --name ${CONTAINER_NAME} \
                    ${DOCKER_IMAGE}
                """
            }
        }
        
        stage('Health Check') {
            steps {
                script {
                    sh """
                        sleep 10
                        curl -f http://localhost:5000
                    """
                }
            }
        }
    }
}