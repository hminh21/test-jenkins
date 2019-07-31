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

  stages {
    stage('Remove PR in workspace') {
        when {
            expression {
                return env.action == "closed"
            }
        }

        steps {
            script {
                if (!utils.removePullRequest("f9740fa6-1539-43d5-ad6b-eae3ddbf2e9d")) {
                    currentBuild.result = "FAILURE"
                }
                //Remove builds manually
                dir("${env.WORSPACE}") {
                    dir("../../") {
                        dir("jobs/kobiton/jobs/${repo}/branches/PR-${number}") {
                            deleteDir()
                        }
                    }
                }
            }
        }
    }
  }
}
