pipeline {
  agent {
    label 'jenkins-slave-java'
  }
  stages {
    stage('Show Parameters'){
        steps{
            sh 'echo ${GIT_COMMIT}'
        }
    }
    stage('Build'){
        steps{
            sh 'mvn package'
        }
    }
  }
  post {
    always {
      echo "Job execution complete."
    }
    success {
      archiveArtifacts artifacts: 'single-module/target/*'
      archiveArtifacts artifacts: 'multi-module/target/*'
    }
    unsuccessful {
      echo "Job execution status is failed, please check error logs"
    }
    cleanup {
      echo 'Cleaning up environment'
      sh 'rm -rf maven-samples'
    }
  }
}
