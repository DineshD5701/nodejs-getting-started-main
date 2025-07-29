pipeline {
    agent any

    tools {
        nodejs "NodeJS" // Must match name in Global Tool Configuration
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/DineshD5701/nodejs-getting-started-main.git',
                        credentialsId: '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' 
                    ]]
                ])
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
                junit 'test-results/*.xml' // optional, only if your tests generate JUnit reports
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
