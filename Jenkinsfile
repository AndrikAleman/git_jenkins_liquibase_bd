pipeline {
    agent any

    tools {
        liquibase 'liquibase-4.30'
    }

    environment {
        ${LIQUIBASE_HOME}/liquibase \
        --logLevel=debug \
        --url=jdbc:postgresql://localhost:5432/test01 \
        --username=andrik \
        --password=$PGPASSWORD
        PGPASSWORD = 'master'
        --changelogFile=liquibase/changelog-master.xml
        update
    }

    stages {

        stages('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AndrikAleman/git_jenkins_liquibase_bd.git'
            }
        }

        stages('Debug Liquibase') {
            steps {
                sh 'echo Workspace: $WORKSPACE'
                sh 'ls -la'
                sh 'pwd'
                sh 'cat changelog-master.xml '
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