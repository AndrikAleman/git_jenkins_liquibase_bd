node {

    pipeline {
        agent any

        tools {
            liquibase 'liquibase-4.30'
        }

        environment {
            PGPASSWORD = 'master'
        }

        stages {

            stage('Checkout') {
                steps {
                    git branch: 'main', url: 'https://github.com/AndrikAleman/git_jenkins_liquibase_bd.git'
                }
            }

            stage('Validar archivos') {
                steps {
                    sh "echo 'Archivos en el workspace:'"
                    sh "ls -la"
                    sh "echo 'Archivos en liquibase:'"
                    sh "ls -la liquibase"
                    sh "echo 'Archivos en liquibase/changes:'"
                    sh "ls -la liquibase/changes"
                }
            }

            stage('Actualizar Base') {
                steps {
                    sh """
                        liquibase \
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

}