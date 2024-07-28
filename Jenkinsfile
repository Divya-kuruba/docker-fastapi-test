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
        FASTAPI_PID_FILE = '/tmp/fastapi_app.pid'
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

        

        
        stage('Start FastAPI App') {
            steps {
                // Start your FastAPI application
                //sh "${VENV_DIR}/bin/uvicorn app.main:app --reload --port=8000 --host=0.0.0.0"
                script {
                    // Start FastAPI in the background and save the PID
                    sh """
                    uvicorn app.main:app --host 0.0.0.0 --port 8000 & echo \$! > ${env.FASTAPI_PID_FILE}
                    """
                    sleep 30
                }
            }
        }
        

        
    }

    post {
        always {
            // Cleanup actions
            echo 'Cleaning up...'
            sh 'rm -f ${env.FASTAPI_PID_FILE}'
        }
        
        success {
            echo 'Pipeline completed successfully!'
        }
        
        failure {
            echo 'Pipeline failed!'
        }
    }

}
