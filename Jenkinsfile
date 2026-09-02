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
                echo 'Running tests'
                echo 'Running automated tests'
                sh 'python3 -m pytest'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating artifact'
                sh 'tar -czf devops-demo.tar.gz app/'
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
