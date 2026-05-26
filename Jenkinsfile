pipeline {
    agent any

    stages {

        stage('Run Postman Collection') {
            steps {

                bat 'newman run PetStore.postman_collection.json -e QA.postman_environment.json -r cli,html --reporter-html-export newman-report.html'

            }
        }
    }

    post {

        success {

            emailext(
                subject: "SUCCESS: API Tests Passed",
                body: """
                Postman collection executed successfully.

                Job Name: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}

                Check Console Output:
                ${env.BUILD_URL}
                """,
                to: "madhusudhankareti09@gmail.com",
                attachmentsPattern: 'newman-report.html'
            )

            echo 'Postman Collection Executed Successfully'
        }

        failure {

            emailext(
                subject: "FAILED: API Tests Failed",
                body: """
                Postman collection execution failed.

                Job Name: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}

                Check Console Output:
                ${env.BUILD_URL}
                """,
                to: "madhusudhankareti09@gmail.com",
                attachmentsPattern: 'newman-report.html'
            )

            echo 'Postman Collection Failed'
        }

        always {

            archiveArtifacts artifacts: 'newman-report.html', fingerprint: true

        }
    }
}