pipeline {
    agent any

    environment {
        NODE_VERSION = '22.x'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                git branch: 'main', url: 'https://github.com/Iliya1914/Iliya1914-StudentRegistryAppCI'
            }
        }

        stage('Set Up Node.js') {
            steps {
                echo 'Using system Node.js...'
                bat 'node -v'
                bat 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Start Application') {
            steps {
                echo 'Starting the application...'
                bat 'start /b npm start'
                sleep 10 // Wait for the application to start
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                bat 'npm test'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
            script {
                try {
                    bat 'FOR /F "tokens=2" %A IN (\'tasklist ^| findstr "node"\') DO taskkill /F /PID %A'
                } catch (err) {
                    echo 'No running Node.js process found to kill.'
                }
            }
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
