
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
                sh 'test -f index.html'
                sh 'grep -q "CI/CD Pipeline Demo" index.html'
                echo 'HTML validation passed!'
            }
        }

        stage('Build') {
            steps {
                sh 'mkdir -p build'
                sh 'cp index.html build/'
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
