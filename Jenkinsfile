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
        }

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