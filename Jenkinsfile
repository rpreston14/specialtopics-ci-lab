pipeline{
  agent any
  stages{
      stage('checkout sources') {
        steps{
            git url: 'https://github.com/rpreston14/specialtopics-ci-lab'
        }
      }
      // collect test results
      stage('Test') {
        steps {
          // you should add a test report here
          withMaven (maven: 'maven3') {
            sh "mvn package"
          }
         }
      }
  }
  post {
    always {
      archiveArtifacts artifacts: '**/*.jar', fingerprint: true
      junit '**/*.xml'
    }
  }
}