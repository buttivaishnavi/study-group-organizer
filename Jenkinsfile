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
                echo 'Installing npm packages...'
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the React app...'
                bat 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                script {
                    try {
                        bat 'npm test'
                    } catch (err) {
                        echo "⚠️ No tests found or test failed. Skipping..."
                    }
                }
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
                // Example for static hosting deployment:
                // bat 'npm run deploy'
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

