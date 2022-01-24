pipeline {
    agent {
        docker {
            image 'buildkite/puppeteer'
        }
    }
    environment {
        DD_API_KEY=credentials('DATADOG-API-KEY')
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
                echo 'DD-API-KEY= ${env.DD-API-KEY}'
                echo 'DD-ENV= ${env.DD-ENV}'
                sh 'npm run test'
            }
        }
    }
}
