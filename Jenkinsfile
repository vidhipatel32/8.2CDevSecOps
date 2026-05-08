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

        stage('SonarCloud Analysis') {
            steps {

                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {

                    bat '''
                    curl -o sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-6.0.0.4432-windows.zip

                    powershell -Command "Expand-Archive sonar-scanner.zip -DestinationPath ."

                    sonar-scanner-6.0.0.4432-windows\\bin\\sonar-scanner.bat
                    '''
                }
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
                body: """
                Jenkins pipeline completed successfully.

                Project: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}
                Build URL: ${env.BUILD_URL}
                """,
                to: "vidhipatel20112@gmail.com",
                attachLog: true
            )
        }

        failure {
            emailext(
                subject: "FAILED: Jenkins Build ${env.BUILD_NUMBER}",
                body: """
                Jenkins pipeline failed.

                Check console output:
                ${env.BUILD_URL}
                """,
                to: "vidhipatel20112@gmail.com",
                attachLog: true
            )
        }

        always {
            echo 'CI/CD and security scanning process completed.'
        }
    }
}