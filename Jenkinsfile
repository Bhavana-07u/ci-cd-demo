
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                bat 'if not exist index.html exit /b 1'
                bat 'findstr /C:"CI/CD Pipeline Demo" index.html >nul'
                echo 'HTML validation passed!'
            }
        }

        stage('Build') {
            steps {
                bat 'if not exist build mkdir build'
                bat 'copy /Y index.html build\\index.html'
                echo 'Build completed successfully!'
            }
        }

        stage('Deploy') {
            steps {
                archiveArtifacts artifacts: 'build/index.html',
                                 fingerprint: true
                echo 'Application delivered successfully!'
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD pipeline failed. Check the Console Output.'
        }
    }
}
