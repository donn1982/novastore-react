pipeline {
    agent any

    environment {
        REPO_URL = "https://github.com/<yourusername>/novastore-react.git"
        BUILD_DIR = "build"
        DEPLOY_DIR = "/var/www/html"
    }

    stages {
        stage('Checkout') {
            steps {
                // Fetch code from GitHub
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                // Build the React app
                sh 'npm run build'
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                // Archive build folder in Jenkins
                archiveArtifacts artifacts: "${BUILD_DIR}/**/*", fingerprint: true
            }
        }

        stage('Deploy to Nginx') {
            steps {
                // Deploy build folder to /var/www/html (mapped to Nginx)
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
