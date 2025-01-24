# DevOps Container Workflow

```bash
python3 -m venv .venv
source .venv/bin/activate

source .venv/Scripts/activate # for windows

pip install -r requirements.txt

```

## Jenkins and Flask Docker Setup

This project demonstrates how to set up Jenkins and deploy a Flask application using Docker.

### Prerequisites
- Docker and Docker Compose installed.
- Jenkins installed as a container.

### Steps

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd jenkins-flask-docker-setup
   ```
2. **Start Services with Docker Compose**:
    - Start Jenkins and Flask app:
    ```docker-compose up -d```
3. **Access Jenkins**:
    - Open your browser and go to `http://localhost:8080`.
    - Retrieve the admin password: `docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword`
    - Unlock Jenkins using the initial admin password found in the Jenkins container logs.
    - Install the suggested plugins.
    - Create an admin user.
4. **Build and Deploy**:
    - Trigger the pipeline to build and deploy the Flask application.
    - Access the Flask application at `http://localhost:5000`.

5. **Set Up Jenkins Pipeline**:
    - Create a new pipeline in Jenkins.
    - Copy the Jenkinsfile content into the pipeline script.
