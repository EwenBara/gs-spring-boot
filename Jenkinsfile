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

    stage('Unit test') {
      steps {
        dir(path: 'complete') {
          sh 'mvn test'
          junit 'target/surefire-reports/*.xml'
        }

      }
    }

    stage('Build Candidate') {
      parallel {
        stage('Package') {
          steps {
            dir(path: 'complete') {
              sh 'mvn package'
              archiveArtifacts 'target/**/*.jar'
            }

          }
        }

        stage('Version tag') {
          steps {
            sh 'git tag $(date +%Y%m%d)BC'
          }
        }

      }
    }

  }
}