pipeline {
  agent any
  stages {
    stage('Tomcat') {
      steps {
        sh '''pipeline {
    agent any

    stages {
        stage(\'Build\') {
            steps {
                echo \'Compilando proyecto...\'
                // Aquí iría el comando real para compilar tu proyecto, por ejemplo con Maven:
                // sh \'mvn clean package\'
            }
        }

        stage(\'Deploy to Tomcat\') {
            steps {
                echo \'Desplegando en Tomcat...\'
                withCredentials([usernamePassword(credentialsId: \'tomcat-credenciales\', usernameVariable: \'TOMCAT_USER\', passwordVariable: \'TOMCAT_PASS\')]) {
                    sh """
                    curl -u $TOMCAT_USER:$TOMCAT_PASS \\
                    --upload-file target/miapp.war \\
                    http://localhost:8080/manager/text/deploy?path=/miapp&update=true
                    """
                }
            }
        }
    }
}
'''
        }
      }

    }
  }