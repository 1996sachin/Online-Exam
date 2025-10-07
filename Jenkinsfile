pipeline {
    agent any

    environment {
        BACKEND_DIR = "backend"
        FRONTEND_DIR = "frontend"
        DEPLOY_DIR = "/var/www/online-exam" // change to your web root
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code..."
                checkout scm
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir("${BACKEND_DIR}") {
                    echo "Installing backend dependencies..."
                    sh 'npm install || true'
                }
            }
        }

        stage('Install Frontend Dependencies & Build') {
            steps {
                dir("${FRONTEND_DIR}") {
                    echo "Installing frontend dependencies..."
                    sh 'npm install || true'
                    sh 'npm run build || true'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying backend..."
                sh """
                mkdir -p ${DEPLOY_DIR}/backend
                cp -r ${BACKEND_DIR}/* ${DEPLOY_DIR}/backend/
                """

                echo "Deploying frontend..."
                sh """
                mkdir -p ${DEPLOY_DIR}/frontend
                cp -r ${FRONTEND_DIR}/build/* ${DEPLOY_DIR}/frontend/
                """
            }
        }

        stage('Start Backend with PM2') {
            steps {
                echo "Starting backend with PM2..."
                sh """
                npm install -g pm2 || true
                pm2 stop online-exam-backend || true
                pm2 delete online-exam-backend || true
                pm2 start ${DEPLOY_DIR}/backend/app.js --name online-exam-backend
                pm2 save
                """
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}
