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

  }
}