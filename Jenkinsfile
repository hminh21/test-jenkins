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
        stage('List all PR') {
            steps {
                script {
                    String res = sh(script: 'curl -s -X GET --header "Content-Type: application/json" https://api.github.com/repos/hminh21/test-jenkins/pulls?state=closed', returnStdout: true)
                    def jsonSlurper = new JsonSlurper()
                    def data = jsonSlurper.parseText(res.substring(1, res.length() - 2))
                    //def data = readJSON text: res
                    echo data[0]
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
