pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Install Newman (if not installed) on Windows
                    //bat 'npm install -g newman'
                    def newmanInstalled = false
                    try {
                        // Check if Newman is installed by running `newman --version`
                        bat 'newman --version'
                        newmanInstalled = true
                    } catch (Exception e) {
                        echo 'Newman is not installed, installing now...'
                    }

                    // If Newman is not installed, install it
                    if (!newmanInstalled) {
                        bat 'npm install -g newman'
                    }
                }
            }
        }

        stage('Run Postman Tests') {
            steps {
                script {
                    // Run the Postman tests using Newman
                    bat 'newman run ToolsRental.postman_collection.json -g workspace.postman_globals.json --reporters html --reporter-html-export newman\\report.html'
                }
            }
        }

        stage('Publish HTML Report') {
            steps {
                // Archive the HTML report generated by Newman (using Windows path separator)
                archiveArtifacts artifacts: 'newman\\report.html', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Actions to perform after the pipeline finishes (e.g., notifications or cleanup)
            echo 'Pipeline finished'
            // Publish the HTML report so it appears on the Jenkins job page
            publishHTML(target: [
                reportName: 'Postman Test Report',
                reportDir: 'newman',
                reportFiles: 'report.html',
                keepAll: true
            ])
        }

        success {
            echo 'Postman tests passed successfully!'
        }

        failure {
            echo 'Postman tests failed, check the report for details.'
        }

     
            
      
    }
}
