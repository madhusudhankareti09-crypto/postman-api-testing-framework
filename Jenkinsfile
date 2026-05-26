pipeline {
    agent any

    stages {

        stage('Run Postman Collection') {
            steps {

                bat 'newman run PetStore.postman_collection.json'

            }
        }
    }

    post {

        success {
            echo 'Postman Collection Executed Successfully'
        }

        failure {
            echo 'Postman Collection Failed'
        }
    }
}