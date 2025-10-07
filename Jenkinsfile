pipeline {
    agent any

    environment {
        REPO_URL = "https://github.com/donn1982/novastore-react.git"
        BUILD_DIR = "build"
        DEPLOY_DIR = "/var/www/html"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'node -v'
                sh 'npm -v'
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                // Clean old files before deploying new build
                sh 'rm -rf ${DEPLOY_DIR}/*'
                sh 'cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/'
            }
        }
    }

    post {
        success {
            echo '✅ React App Built and Deployed Successfully via Jenkins!'
        }
        failure {
            echo '❌ Build or Deployment Failed!'
        }
    }
}
