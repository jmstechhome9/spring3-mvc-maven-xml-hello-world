pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        git(url: 'https://github.com/jmstechhome9/spring3-mvc-maven-xml-hello-world.git', branch: 'master', credentialsId: 'github_credentials')
      }
    }

  }
}