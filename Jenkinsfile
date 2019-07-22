pipeline {
    agent any

    stages {
        stage('Checking PR if it is closed...'){
            /*when {
                expression {
                    return env.CHANGE_ID && pullRequest.state == 'open'
                }
            }*/

            steps {
                sh("printenv")
                script {
                    echo "Removing closed PR ${env.BRANCH_NAME}"
                }

            }
        }
    }
}
