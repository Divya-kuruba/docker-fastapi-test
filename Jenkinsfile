pipeline {
    agent any

    environment {
        // Define environment variables
        SERVER_USER = 'ubuntu'
        SERVER_HOST = '13.232.241.115'
        SERVER_PATH = '/path/to/deployment/directory'
        SSH_KEY = credentials('jenkins') // Jenkins credentials ID for SSH private key
        VENV_DIR = '.venv'
        PYTHON_VERSION = 'python3' // Change to 'python' if it points to Python 3 on your agent
        //REPO_URL = 'https://github.com/yourusername/your-python-repo.git'
    }

    stages {
        
        
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                git branch: 'main', url: 'https://github.com/Divya-kuruba/docker-fastapi-test'
            }
        }

        stage('Setup Environment') {
            steps {
                script {
                    // Set up a Python virtual environment
                    sh "${PYTHON_VERSION} -m venv ${VENV_DIR}"
                    sh "${VENV_DIR}/bin/pip install --upgrade pip"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install dependencies from requirements.txt
                sh "${VENV_DIR}/bin/pip install -r requirements.txt"
            }
        }

        

        stage('Build') {
            steps {
                // Optionally build your application or package it
                echo 'Building the application...'
            }
        }

        stage('Deploy application') {
            steps {
                // Set up a virtual environment and install dependencies
                sh 'uvicorn main:app --reload --port=8000 --host=0.0.0.0'
                
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
