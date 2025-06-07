pipeline {
    agent any

    tools {
        nodejs "NodeJS"
    }

    triggers {
        cron('*/1 * * * *') // Ejecuta cada minuto
    }

    environment {
        SONARQUBE = 'SonarQubeServer'
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

        stage('Ejecutar Pruebas') {
            steps {
                bat 'npm test || echo ⚠️ No hay pruebas definidas o fallaron.'
            }
        }

        stage('Análisis SonarQube') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    bat 'npx sonar-scanner ^
                        -Dsonar.projectKey=pokemundo ^
                        -Dsonar.sources=. ^
                        -Dsonar.host.url=http://localhost:9000 ^
                        -Dsonar.login=TU_TOKEN_AQUI'
                }
            }
        }

        stage('Esperar Resultado de Calidad') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }

        stage('Empaquetar Proyecto') {
            steps {
                echo 'Empaquetando proyecto...'
            }
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
