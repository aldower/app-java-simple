@Library('my-shared-library') _
pipeline {
    agent {
        docker {
            image 'maven:3.9.4-eclipse-temurin-17'
            args '-v $HOME/.m2:/root/.m2'
        }
    }

    environment {
        APP_NAME  = 'app-java-simple'
        APP_VERSION = '1.0'
    }

    stages {

        stage('Checkout') {
            steps {
                echo "📥 Clonando repositorio: ${env.APP_NAME}"
                checkout scm
            }
        }

        stage('Compilar') {
            steps {
                buildJava()
            }
        }

    }

    post {
        success {
            notifyBuild('SUCCESS')
        }
        failure {
            notifyBuild('FAILURE')
        }
    }
}