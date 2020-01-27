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
          sh 'mvn jacoco:report'
          junit 'target/surefire-reports/*.xml'
        }

      }
    }

    stage('Code Quality') {
      steps {
        dir(path: 'complete') {
          sh 'mvn sonar:sonar'
        }
      }
    }

    stage('Build Candidate') {
      parallel {
        stage('Package') {
          steps {
            dir(path: 'complete') {
              sh 'mvn -DskipTests package'
              archiveArtifacts 'target/**/*.jar'
            }

          }
        }

        stage('Version tag') {
          steps {
            withCredentials([usernamePassword(credentialsId: '7c42fcf2-6fd7-408f-942b-bf0581980fca', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
              sh('git tag -a ${BUILD_TIMESTAMP}BC')
              sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${GIT_URL} --tags')
            }
          }
        }

      }
    }

  }
}