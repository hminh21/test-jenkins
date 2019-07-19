import groovy.json.JsonSlurper
import groovy.json.JsonOutput

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
                    def res = sh(script: 'curl -u hminh21:1eecd9c7d85fc4af82a6101ba301fcb50bdc4129 -s https://api.github.com/repos/hminh21/test-jenkins/pulls?state=all', returnStdout: true)
                    //def jsonSlurper = new JsonSlurper()
                    //def data = jsonSlurper.parseText("${res}")
                    echo res
                    //echo data
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
