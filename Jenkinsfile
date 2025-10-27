pipeline {
    agent any

    tools {
        // Optional: if you configured Python under "Global Tool Configuration"
        // python 'Python'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/riks17/py-selenuim-test.git'
            }
        }

        stage('Setup Environment') {
            steps {
                // Use the Python launcher (works better on Windows)
                bat '''
                    py -3 -m venv venv
                    call venv\\Scripts\\activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                    call venv\\Scripts\\activate
                    pytest tests/ --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Publish Results') {
            steps {
                echo 'Selenium Tests completed successfully!'
            }
        }
    }

    post {
        failure {
            echo 'Build failed. Please check console output for details.'
        }
    }
}
