
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm packages... add dependency'
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the React app...'
                bat 'npm run build'
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                echo 'Archiving build output...'
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying build...'
                // bat 'npm run deploy'  // optional
            }
        }
    }

    post {
        success {
            echo '✅ Build and pipeline completed successfully.'
        }
        failure {
            echo '❌ Build or test failed.'
        }
    }
}
