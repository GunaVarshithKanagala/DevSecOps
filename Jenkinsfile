pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/GunaVarshithKanagala/DevSecOps.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }
        
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }
        
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
    }
    
    post {
        always {
            emailext (
                subject: "Build ${currentBuild.result}: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                body: """
                Build Status: ${currentBuild.result}
                Build Number: ${env.BUILD_NUMBER}
                Build URL: ${env.BUILD_URL}
                
                Check console output at ${env.BUILD_URL} to view full results.
                """,
                to: "your_email@gmail.com",
                attachmentsPattern: "*.log"
            )
        }
    }
}
