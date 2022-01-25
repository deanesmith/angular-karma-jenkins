pipeline {
    agent {
        docker {
            image 'buildkite/puppeteer'
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Preparing...'
                sh 'npm install'
                echo 'Building...'
                sh 'npm run build'
            }
        }
        stage('Test') {
            environment {
                DATADOG_API_KEY=credentials('DATADOG-API-KEY')
                DD_ENV='ci'
                DD_SERVICE='bodata'
                DD_TEST_RESULTS_DIR='unit-test-results'
            }
            steps {
                echo 'Testing...'
                sh 'npm run test'
                sh """ echo "Build number in sh script: ${env.DATADOG_API_KEY} """
                sh './node_modules/.bin/datadog-ci junit upload --service bodata ./unit-test-results'
            }
        }
    }
}
