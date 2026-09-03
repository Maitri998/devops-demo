pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building application'
                sh 'python3 app/app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests'
                sh '''
                    python3 -m venv .venv
                    .venv/bin/python -m pip install --upgrade pip
                    .venv/bin/pip install pytest
                    .venv/bin/python -m pytest
                '''
            }
        }

        stage('Package') {
            steps {
                echo 'Creating artifact'
                sh 'tar -czf devops-demo.tar.gz app/'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t devops-demo:1.0 .'
            }
        }

        stage('Docker Run') {
            steps {
                echo 'Running Docker container'
                sh 'docker run --rm devops-demo:1.0'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
