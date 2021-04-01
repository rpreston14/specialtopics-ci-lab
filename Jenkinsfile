
node {
  stage('checkout sources') {
        // You should change this to be the appropriate thing
        git url: 'https://github.com/rpreston14/specialtopics-ci-lab'
  }

  stage('Build') {
    // you should build this repo with a maven build step here
    echo "hello"
  }
  // you should add a test report here
  withMaven (maven: 'maven3') {
  sh "mvn package"
  }
  // collect test results
   agent any
    stages {
        stage('Test') {
            steps {
                sh './gradlew check'
            }
        }
    }
    post {
        always {
            junit 'build/reports/**/*.xml'
        }
    }
}
