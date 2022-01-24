pipeline {
    agent {
        docker {
            image 'buildkite/puppeteer'
        }
    }
    environment {
        DATADOG_API_KEY=credentials('DATADOG-API-KEY')
        DATADOG_SITE='datadoghq.com'
        DD_ENV='ci'
        DD_SERVICE='bodata'
        DD_TEST_RESULTS_DIR='unit-test-results'
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
            steps {
                echo 'Testing...'
                echo ${env.DD-API-KEY}
                echo ${env.DATADOG_SITE}
                echo ${env.DD-ENV}
                echo ${env.DD_SERVICE}
                echo ${env.DD_TEST_RESULTS_DIR}
                sh 'npm run test'
            }
        }
    }
}
