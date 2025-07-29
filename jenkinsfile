pipeline {
    agent any

    tools {
        nodejs "NodeJS" // defined under Jenkins -> Global Tool Configuration
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/heroku/node-js-sample.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Archive Test Reports') {
            steps {
                junit 'test-results/*.xml' // Assuming mocha or similar output
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Build and test successful.'
        }
        failure {
            echo 'Build failed. Check logs and test results.'
        }
    }
}

