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
                echo 'Setting up Node.js...'
                script {
                    // Use the NodeJS plugin in Jenkins
                    def nodeHome = tool name: "NodeJS ${NODE_VERSION}", type: 'NodeJS'
                    env.PATH = "${nodeHome}/bin:${env.PATH}"
                }
                sh 'node -v'
                sh 'npm -v'
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
                bat 'npm start &'
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
            bat 'kill $(lsof -t -i:3000) || true' // Ensure the application is stopped (adjust port as needed)
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
