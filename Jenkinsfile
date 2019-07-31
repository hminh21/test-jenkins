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
     regexpFilterText: '$action kobiton/$repo/PR-$number',
     regexpFilterExpression: 'closed ' + JOB_NAME,
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
                 dir("${env.WORKSPACE}") {
      deleteDir()
    }

    //Sometimes the build will create more workspace such as library, temp or script.
    //The WORKSPACE env only points to the original one so that we have to delete other extension manually
    dir("${env.WORKSPACE}@libs") {
      deleteDir()
    }

    dir("${env.WORKSPACE}@script") {
      deleteDir()
    }
    
    dir("${env.WORKSPACE}@script@tmp") {
      deleteDir()
    }

    dir("${env.WORKSPACE}@tmp") {
      deleteDir()
    }
                if (!utils.removePullRequest("f9740fa6-1539-43d5-ad6b-eae3ddbf2e9d")) {
                    currentBuild.result = "FAILURE"
                } 
            }
        }

        /*post {
            failure {
                script {
                    echo "fail"
                }
            }

            success {
                script {
                    echo "success"
                }
            }
        }*/
    }
  }
}
