pipeline{
  agent any
  stages{
      stage('checkout sources') {
        steps{
            git url: 'https://github.com/rpreston14/specialtopics-ci-lab'
        }
      }
      stage('Build') {
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