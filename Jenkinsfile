pipeline{
node {
  stage('checkout sources') {
        // You should change this to be the appropriate thing
        git url: 'https://github.com/rpreston14/specialtopics-ci-lab'
  }
  agent any
  stages{
      stage('Build') {
        // you should build this repo with a maven build step here
        steps {
           sh './gradlew build'
        }
      }
      // you should add a test report here
      withMaven (maven: 'maven3') {
        sh "mvn package"
      }
      // collect test results
      stage('Test') {
        steps {
           sh './gradlew check'
         }
      }
  }
  post {
    always {
      archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
      junit 'build/reports/**/*.xml'
    }
  }
}
}