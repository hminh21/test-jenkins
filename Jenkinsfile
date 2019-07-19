pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Checking PR if it is closed...'){
            when {
                expression {
                    return env.CHANGE_ID && pullRequest.status == 'closed'
                }
            }

            environment {

            }

            steps {
                sh("printenv")
                script {
                    echo 'Removing closed PR ${env.BRANCH_NAME}'
                }
            }
        }
    }
}
