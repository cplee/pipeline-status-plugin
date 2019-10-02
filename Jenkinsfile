//library 'pipeline-library'
library 'LEAD'

pipeline {
  agent any
  stages {
    stage('Maven Package and Deploy') {
      agent {
        label "lead-toolchain-maven"
      }
      when {
        branch 'master'
      }
      steps {
        notifyPipelineStart([Jenkinsfile: 'Jenkinsfile'])
        notifyStageStart()
        container('maven') {
          sh 'mvn package deploy'
        }
      }
      post {
        success {
          notifyStageEnd()
        }
        failure {
          notifyStageEnd([result: "fail"])
        }
      }
    }
  }
  post {
    success {
      echo "Pipeline Success"
      notifyPipelineEnd()
    }
    failure {
      echo "Pipeline Fail"
      notifyPipelineEnd([result: "fail"])
    }
  }
}
