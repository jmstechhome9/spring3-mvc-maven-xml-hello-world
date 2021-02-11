pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'mvn package'
      }
    }

    stage('artifact') {
      steps {
        sh 'archiveArtifacts \'target/*.war\''
      }
    }

  }
}