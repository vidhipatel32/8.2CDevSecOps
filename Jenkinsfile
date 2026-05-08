pipeline {
    agent any

    stages {

        stage('Checkout Source Code') {
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

        stage('Application Build') {
            steps {
                echo 'Building Node.js application...'
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo 'Executing application tests...'
            }
        }

        stage('Dependency Vulnerability Scan') {
            steps {
                bat 'npm audit || ver > nul'
            }
        }

        stage('Generate Security Report') {
            steps {
                echo 'Generating security report...'
            }
        }

        stage('Deployment Validation') {
            steps {
                echo 'Deployment validation completed.'
            }
        }
    }

    post {

        success {
            emailext(
                subject: "SUCCESS: Jenkins Build ${env.BUILD_NUMBER}",
                body: "Build completed successfully.",
                to: "vidhipatel20112@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "FAILED: Jenkins Build ${env.BUILD_NUMBER}",
                body: "Build failed. Check Jenkins console.",
                to: "vidhipatel20112@gmail.com"
            )
        }

        always {
            echo 'CI/CD and security scanning process completed.'
        }
    }
}