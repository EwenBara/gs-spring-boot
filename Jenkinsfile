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
            sh '''git tag ${BUILD_TIMESTAMP}BC
git push --tags'''
          }
        }

      }
    }

  }
}