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
        stage('List all PR')
        {
            steps{
                script
                {
                    def res = sh(script: 'curl -s https://api.github.com/repos/hminh21/test-jenkins/pulls?state=all')
                    echo res
                }
            }
        }
        /*stage('Checking PR if it is closed...'){
            when {
                expression {
                    return env.CHANGE_ID && pullRequest.state == 'open'
                }
            }

            steps {
                sh("printenv")
                script {
                    echo 'Removing closed PR ' ${env.BRANCH_NAME}
                }
            }
        }*/

    }
}
