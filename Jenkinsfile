@Library("minh-pipeline@master") _

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
  
  stages {
    stage('print env') {
      steps {
        script {
             sh('printenv') 
        }
      }
    }
    stage('Remove PR in workspace') {
        when {
            expression {
                return env.action == "closed"
            }
        }
        steps {
            script {
                if (!utils.removePullRequest("f9740fa6-1539-43d5-ad6b-eae3ddbf2e9d")) {
                    error("Fail")
                    //currentBuild.result = "FAILURE"
                }
            }
        }
    }
  }
}
