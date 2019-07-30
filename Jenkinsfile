pipeline {
  agent any
 triggers {
    GenericTrigger(
     genericVariables: [
      [key: 'action', value: '$.action'],
      [key: 'number', value: '$.number'],
      [key: 'repo', value: '$.repository.name'],
      [key: 'branch', value: '$.pull_request.base.ref']
     ],
     token: 'TriggerPR',
     causeString: 'Triggered on $action Pull Request',
     regexpFilterText: '$action kobiton/$repo/$branch',
     regexpFilterExpression: 'closed ' + JOB_NAME,
     printContributedVariables: true,
     printPostContent: true
    )
 }

 environment {
    PR_WORKSPACE_DIRECTORY = "${env.JENKINS_HOME}/jobs/kobiton/jobs/${env.repo}/branches/PR-${env.number}"
 }

  stages {
    stage('Remove PR in workspace') {
        steps {
            script {
                if (env.repo == "booster-automated-execution-runner") {
                    PR_WORKSPACE_DIRECTORY = "${env.JENKINS_HOME}/jobs/kobiton/jobs/booster-auto.1vadu4.ution-runner/branches/PR-${env.number}"
                }

                sh "printenv"
                echo "${env.PR_WORKSPACE_DIRECTORY}"

                if (fileExists(env.PR_WORKSPACE_DIRECTORY)) {
                    dir("${env.PR_WORKSPACE_DIRECTORY}")
                    {
                        deleteDir()
                        echo "Removed at ${env.PR_WORKSPACE_DIRECTORY}"
                        //echo "PR-${env.number} in ${env.repo} has been cleaned"
                    }
                }
                else {
                    error("CLEANING FAIL BECAUSE PR DOES NOT EXIST IN WORKSPACE")
                }
            }
        }
    }
  }
  
  post {
      success {
          script {
              withCredentials([string(credentialsId: 'f9740fa6-1539-43d5-ad6b-eae3ddbf2e9d', variable: 'API_TOKEN')]) {
             //Get Jenkins-Crumb
             resJson = sh(script: "curl -s -u hminh21:${API_TOKEN} https://dbe5b623.ngrok.io/crumbIssuer/api/json", returnStdout: true)
             def res = readJSON text: resJson
             
             //Do delete job in jenkins
             statusCode = sh(script: "curl -f --show-error -s -X POST -u hminh21:${API_TOKEN} -H 'Jenkins-Crumb:${res['crumb']}' https://dbe5b623.ngrok.io/job/kobiton-inc/job/${env.repo}/view/change-requests/job/PR-${env.number}/doDelete", returnStatus: true)

             if (statusCode == 0) {
                 echo "PR-${env.number} job in ${env.repo} has been deleted"
                 }
             else {
                 echo "REMOVING JOB FAIL BECAUSE OF SENDING TO REST API JENKINS FAIL"
                 currentBuild.result = "FAILURE"
                }
              }
            }
        }
    }
}
