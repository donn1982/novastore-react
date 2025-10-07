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

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: "${BUILD_DIR}/**/*", fingerprint: true
            }
        }

        stage('Deploy to Nginx') {
            steps {
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
