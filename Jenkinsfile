pipeline {
    agent any

    environment {
        PGPASSWORD = 'master'
        LIQUIBASE_HOME = '/opt/liquibase'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AndrikAleman/git_jenkins_liquibase_bd.git'
            }
        }

        stage('Validar archivos') {
            steps {
                sh "ls -la"
                sh "ls -la liquibase"
                sh "ls -la liquibase/changes"
            }
        }

        stage('Actualizar Base') {
            steps {
                sh """
                    ${LIQUIBASE_HOME}/liquibase \
                        --defaultsFile=liquibase/liquibase.properties \
                        update
                """
            }
        }
    }

    post {
        success {
            echo 'Liquibase update se ejecutó correctamente.'
        }
        failure {
            echo 'Liquibase update falló, revisar logs.'
        }
    }
}