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
                    def res = sh(script: 'curl -u hminh21:4d588457306497f940f481efc73312168a3ba511 -s https://api.github.com/repos/hminh21/test-jenkins/pulls?state=closed', returnStdout: true)
                    def jsonSlurper = new JsonSlurper()
                    def data = jsonSlurper.parseText("${res}")
                    echo data[0].number
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
