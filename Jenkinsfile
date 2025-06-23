pipeline {
    agent any
    stages {
        stage('Source') {
            steps {
                git 'https://github.com/hollmanlp/unir-cicd.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Construyendo Build'
                script {
                    sh 'make build'
                }
            }
        }
        stage('Unit Test') {
            steps {
                echo 'Unit Test stage'
                sh 'make test-unit'
                archiveArtifacts artifacts: 'results/*.xml', allowEmptyArchive: true
            }
        }
        stage('Unit Test-API') {
            steps {
                echo 'Unit Test stage'
                sh 'make test-api'
                archiveArtifacts artifacts: 'results/*.xml', allowEmptyArchive: true
            }
        }
        stage('Unit Test-E2E') {
            steps {
                echo 'Unit Test stage'
                sh 'make test-e2e'
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
