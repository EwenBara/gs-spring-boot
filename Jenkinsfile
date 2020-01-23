pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        dir(path: 'compile') {
          sh 'mvn compile'
        }

      }
    }

  }
}