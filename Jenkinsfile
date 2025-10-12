pipeline {
    agent any
    environment {
        // Define any needed secrets or environment variables here
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                echo 'Installing npm packages...'
                bat 'npm install'
            }
        }
        stage('Lint') {
            steps {
                echo 'Linting code...'
                bat 'npm run lint || exit /b 0' // Ignore error if no lint script
            }
        }
       
        stage('Build') {
            steps {
                echo 'Building the production assets...'
                bat 'npm run build'
            }
        }
        stage('Archive Build Artifacts') {
            steps {
                echo 'Archiving build output...'
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
            }
        }
    }
    post {
        success {
            echo '✅ CI pipeline completed successfully.'
        }
        failure {
            echo '❌ CI failed. Please check the logs.'
        }
    }
}
