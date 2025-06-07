pipeline {
    agent any

    triggers {
        cron('*/1 * * * *') // Ejecuta cada minuto
    }

    environment {
        SONARQUBE = 'SonarQubeServer' // Nombre del servidor Sonar configurado en Jenkins
    }

    stages {
        stage('Clonar Repositorio') {
            steps {
                git url: 'https://github.com/haroldcj18/pokemundo.git', branch: 'main'
            }
        }

        stage('Instalar Dependencias') {
            steps {
                bat 'npm install'
            }
        }


    post {
        success {
            mail to: 'harold_cortes82172@elpoli.edu.co',
                subject: "✅ Pipeline exitoso - Pokemundo",
                body: "La integración continua finalizó correctamente."
        }
        failure {
            mail to: 'tucorreo@ejemplo.com',
                subject: "❌ Falló el pipeline - Pokemundo",
                body: "Revisa Jenkins para más detalles del error."
        }
    }
}
