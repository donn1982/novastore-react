pipeline {
    agent any

    // Use NodeJS tool configured in Jenkins (Manage Jenkins → Global Tool Configuration → NodeJS)
    tools {
        nodejs "NodeJS 20" // Replace with the exact name you gave your NodeJS installation
    }

    environment {
        REPO_URL = "https://github.com/donn1982/novastore-react.git"
        BUILD_DIR = "build"
        DEPLOY_DIR = "/var/www/html"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Fetching source code from GitHub..."
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing npm dependencies..."
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo "Building React app..."
                sh 'npm run build'
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                echo "Archiving build artifacts..."
                archiveArtifacts artifacts: "${BUILD_DIR}/**/*", fingerprint: true
            }
        }

        stage('Deploy to Nginx') {
            steps {
                echo "Deploying build to Nginx..."
                sh "cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/"
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Completed Successfully!'
        }
        failure {
            echo 'Build or Deployment Failed!'
        }
    }
}
