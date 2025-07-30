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
                        url: 'https://github.com/DineshD5701/nodejs-getting-started-main', //
                        credentialsId: 'github-token' 
                    ]]
                ])
            }
        }

        stage('Install Dependencies') {
        steps {
        sh 'npm install'
        sh 'npm install -g mocha'  // ❗ Avoid unless absolutely needed
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Archive Test Reports') {
            steps {
                junit 'test-results/results.xml'
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
