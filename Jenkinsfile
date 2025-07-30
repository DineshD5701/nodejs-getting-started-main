pipeline {
    agent any

    tools {
        nodejs "NodeJS" // Must match name in Global Tool Configuration
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
