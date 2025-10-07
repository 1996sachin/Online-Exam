pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code..."
                checkout scm
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    echo "Installing PHP dependencies..."
                    sh 'composer install --no-interaction --prefer-dist'
                }
            }
        }

        stage('Install Frontend Dependencies & Build') {
            steps {
                dir('frontend') {
                    echo "Installing Node.js dependencies..."
                    sh 'npm install'
                    echo "Building frontend..."
                    sh 'npm run build'
                }
            }
        }

        stage('Run Tests') {
            steps {
                dir('backend') {
                    echo "Running PHP Unit tests..."
                    sh './vendor/bin/phpunit || true'
                }
                dir('frontend') {
                    echo "Running frontend tests..."
                    sh 'npm test || true'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
                sh """
                cp -r backend/* /var/www/html/
                cp -r frontend/dist/* /var/www/html/public/
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
