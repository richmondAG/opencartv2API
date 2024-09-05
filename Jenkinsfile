pipeline {
    agent any
    environment {
        // Define environment variables for Newman report
        // NEWMAN_REPORT_FILE = 'newman-report.html'
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out repository...'
                // Pull the repository containing your Postman collection
               git 'https://github.com/richmondAG/opencartv2API.git'
            }
        }
        
        stage('Run API Tests') {
            steps {
                echo 'Running API tests using Newman...'
                // Run the Postman collection with Newman (on Windows)
                bat "newman run OpenCartV2.postman_collection.json --reporters cli,html --reporter-html-export ${NEWMAN_REPORT_FILE}"
            }
        }
    }
    
    post {
        always {
            echo 'Archiving test results...'
            // Archive Newman HTML report
            archiveArtifacts artifacts: '${NEWMAN_REPORT_FILE}', allowEmptyArchive: true
        }
        
        success {
            echo 'API tests passed successfully.'
        }
        
        failure {
            echo 'API tests failed.'
        }
    }
}
