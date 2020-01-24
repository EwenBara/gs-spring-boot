pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        dir(path: 'complete') {
          sh 'mvn compile'
        }

      }
    }

    stage('Test') {
      steps {
        dir(path: 'complete') {
          sh 'mvn test'
          junit 'target/surefire-reports/*.xml'
        }

      }
    }

  }

  post {
    always {
      archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
    }
  }
}