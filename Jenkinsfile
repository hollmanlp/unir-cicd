pipeline {
    agent {
        docker {
            image 'python:3.13.5-bookworm'
            args '-u root'    // Ejecutar como root para poder instalar paquetes
        }
    }
    stages {
        stage('Source') {
            steps {
                git 'https://github.com/hollmanlp/unir-cicd.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Construyendo stage'
                script {
                    // Instalación de 'make' dentro del contenedor
                    sh '''
                        apt-get update
                        apt-get install -y make
                        make --version
                    '''
                }
                echo 'Construyendo stage'
                sh 'make build'
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Unit Test stage'
                sh 'make test-unit'
                archiveArtifacts artifacts: 'results/*.xml', allowEmptyArchive: true
            }
        }
    }
    post {
        always {
            junit 'results/*_result.xml'
            cleanWs()
        }
    }
}
