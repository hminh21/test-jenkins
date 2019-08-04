@Library("minh-pipeline@master") _

pipeline {
  agent any
 triggers {
    GenericTrigger(
     genericVariables: [
      [key: 'action', value: '$.action'],
      [key: 'number', value: '$.number'],
      [key: 'repo', value: '$.repository.name']
     ],
     token: 'TriggerPR',
     causeString: 'Triggered on $action Pull Request',
     regexpFilterText: 'kobiton/$repo/PR-$number',
     regexpFilterExpression: JOB_NAME,
     printContributedVariables: true,
     printPostContent: true
    )
 }

   stage('Remove PR in workspace') {
      when {
          expression {
              return env.action == "closed"
          }
      }

      steps {
          script {
              if (!utils.removePullRequest("jenkins-api-token")) {
                  currentBuild.result = "FAILURE"
              }
          }
      }
    }  
}
