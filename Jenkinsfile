pipeline {
    agent any

    environment {
        PHP_VERSION = '7.4'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git url: 'https://github.com/prrs18/prrsinternship.git', branch: 'main'
            }
        }

        stage('Install Composer') {
            steps {
                // Check if Composer is installed, if not, install it
                sh '''
                if ! [ -x "$(command -v composer)" ]; then
                    echo "Installing Composer..."
                    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
                else
                    echo "Composer is already installed"
                fi
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Composer dependencies
                sh 'composer install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run PHP Unit tests
                sh 'vendor/bin/phpunit'
            }
        }

        stage('Static Analysis') {
            steps {
                // Run PHP CodeSniffer for code style checks
                sh 'vendor/bin/phpcs --standard=PSR2 src/'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application
                // Placeholder for actual deployment steps
                sh 'echo "Deploying application..."'
            }
        }
    }

    post {
        always {
            // Clean up the workspace
            cleanWs()
        }

        success {
            // Notify success
            echo 'Build succeeded!'
        }

        failure {
            // Notify failure
            echo 'Build failed!'
        }
    }
}
