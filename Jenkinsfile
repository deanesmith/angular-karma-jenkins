pipeline {
    agent {
        docker {
            image 'buildkite/puppeteer'
        }
    }
    environment {
        DATADOG_API_KEY=credentials('DATADOG-API-KEY')
        DD_ENV='ci'
        DD_SERVICE='bodata'
        DD_TEST_RESULTS_DIR='unit-test-results'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Preparing...'
                sh 'npm install'
                sh 'npm install -g @datadog/datadog-ci'
                echo 'Building...'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm run test'
                sh "datadog-ci junit upload --service bodata /unit-test-results"
            }
        }
    }
}
