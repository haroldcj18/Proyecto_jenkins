pipeline {
  agent any
  stages {
    stage('Tomcat') {
      steps {
        sh '''withCredentials([usernamePassword(credentialsId: \'credenciales_tomcat\', usernameVariable: \'tomcat\', passwordVariable: \'tomcat\')]) {
    sh """
    curl -u $TOMCAT_USER:$TOMCAT_PASS ^
         --upload-file sample.war ^
         http://localhost:8090/manager/text/deploy?path=/miapp&update=true
    """
}
'''
        }
      }

    }
  }
