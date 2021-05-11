pipeline {
    agent any

    tools {nodejs "node"}

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './node_modules/.bin/cypress run'

                sh 'npm run merge-report'

                sh 'npm run generate-report'

                publishHTML (target: [
                             allowMissing: false,
                             alwaysLinkToLastBuild: false,
                             keepAll: true,
                             reportDir: 'cypress/reports',
                             reportFiles: 'report.html',
                             reportName: "RCov Report"
                        ])
            }
        }
    }
}