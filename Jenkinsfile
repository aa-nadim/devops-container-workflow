pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'flask-app'
        CONTAINER_NAME = 'flask-app'
        GITHUB_REPO_URL = 'https://github.com/aa-nadim/devops-container-workflow.git'
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    try {
                        git branch: 'main', 
                            url: "${GITHUB_REPO_URL}",
                            credentialsId: 'your-github-credentials-id'
                        echo "Repository cloned successfully"
                    } catch (Exception e) {
                        error "Failed to clone repository: ${e.message}"
                    }
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    try {
                        sh "docker build --no-cache -t ${DOCKER_IMAGE} ."
                        echo "Docker image built successfully"
                    } catch (Exception e) {
                        error "Docker image build failed: ${e.message}"
                    }
                }
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
                script {
                    try {
                        sh """
                            docker run -d \
                            -p 5000:5000 \
                            --name ${CONTAINER_NAME} \
                            ${DOCKER_IMAGE}
                        """
                        echo "Flask application deployed successfully"
                    } catch (Exception e) {
                        error "Flask application deployment failed: ${e.message}"
                    }
                }
            }
        }
        
        stage('Health Check') {
            steps {
                script {
                    try {
                        sh """
                            sleep 10
                            curl -f http://localhost:5000
                        """
                        echo "Application health check passed"
                    } catch (Exception e) {
                        error "Health check failed: ${e.message}"
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
        always {
            echo 'Pipeline execution completed.'
        }
    }
}