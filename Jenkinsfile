pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    CHARTMUSEUM_CREDS = credentials('jenkins-x-chartmuseum')
    DEPLOY_NAMESPACE = "hhs-int"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          sh 'make build'
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
           sh 'make install'
        }
      }
    }
  }
}
