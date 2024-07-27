pipeline {
    agent any

    environment {
        // Define environment variables
        SERVER_USER = 'ubuntu'
        SERVER_HOST = '13.233.157.159'
        SERVER_PATH = '/path/to/deployment/directory'
        SSH_KEY = credentials('jenkins') // Jenkins credentials ID for SSH private key
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
                // Set up a virtual environment and install dependencies
                
                sh 'python3 -m venv venv'
                sh 'source venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests to make sure everything is working
                sh 'source venv/bin/activate && pytest'
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
