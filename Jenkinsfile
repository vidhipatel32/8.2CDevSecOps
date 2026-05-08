pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/vidhipatel32/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage'
            }
        }

        stage('NPM Audit Security Scan') {
            steps {
                bat 'npm audit'
            }
        }
    }

    post {

        success {
            echo 'DevSecOps pipeline executed successfully.'
        }

        failure {
            echo 'Pipeline execution completed with warnings or vulnerabilities.'
        }

        always {
            echo 'Security scanning process completed.'
        }
    }
}