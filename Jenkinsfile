pipeline {
    agent any

    tools {
        liquibase 'liquibase-4.30'
    }

    environment {
        PGPASSWORD = 'master'
    }

    stages {

        stages('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AndrikAleman/git_jenkins_liquibase_bd.git'
            }
        }

        stages('List JAR'){
            steps {
                sh 'ls -l liquibase/'
            }
        }

        stages {
            steps {
                sh '''
                    liquibase \
                    --defaultFile=liquibase/liquibase.properties \
                    update
                '''
            }
        }
    }

    post {
        success {
            echo 'Liquibase update se ejecuto correctamente.'
        }
        failure {
            echo 'Liquibase update fallo, Revisar logs.'
        }
    }
}