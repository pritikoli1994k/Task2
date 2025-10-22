pipeline {
    agent any

    environment {
        IMAGE_NAME = "imagejenkins"
        CONTAINER_NAME = "containerjenkins"
        PORT = "3100"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                git branch: 'main', url: 'https://github.com/pritikoli1994k/Task2'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Test (Dummy)') {
            steps {
                echo 'Running dummy test...'
                bat 'echo All tests passed successfully!'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying container...'
                bat 'docker rm -f %CONTAINER_NAME% || exit 0'
                bat 'docker run -d --name %CONTAINER_NAME% -p %PORT%:3000 %IMAGE_NAME%:latest'
                bat 'docker logs %CONTAINER_NAME%'
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
            echo "Access your app at http://localhost:%PORT%"
        }
        failure {
            echo 'Build Failed!'
        }
    }
}