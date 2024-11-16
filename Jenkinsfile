pipeline {
    agent any

    environment {
        NODE_VERSION = '16.x' // Update to match your NodeJS installation in Jenkins
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
                echo 'Setting up Node.js...'
                script {
                    def nodeHome = tool name: "NodeJS ${NODE_VERSION}", type: 'NodeJS'
                    env.PATH = "${nodeHome}/bin:${env.PATH}"
                }
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
            bat 'for /f "tokens=5" %a in (\'netstat -ano ^| find ":3000"\') do taskkill /pid %a /f'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
