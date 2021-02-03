pipeline {
    agent any
        tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3"
    }

    stages {
        stage('getscm') {
            steps {
                // Get some code from a GitHub repository
                  git credentialsId: 'github_credentials', url: 'https://github.com/jmstechhome9/spring3-mvc-maven-xml-hello-world.git'            }

        }
         stage('Build') {
            steps {
                // maven package
               sh 'mvn package'
               }
        }
        stage('artifact') {
            steps {

            archiveArtifacts 'target/*.war'
      }

    }
    stage('deploy'){

        steps{

            withCredentials([usernameColonPassword(credentialsId: 'tomcat_credentials', variable: 'tomcatcred')]) {
                sh "curl -v -u ${tomcatcred} -T /var/lib/jenkins/workspace/tomcat_deploy_pipeline/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'http://ec2-52-66-242-116.ap-south-1.compute.amazonaws.com:8081/manager/text/deploy?path=/pipeline_spring&update=true'"

           }
        }
    }

}

 post {
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "jmstechhome@gmail.com",
                sendToIndividuals: true])
        }
    }
}


