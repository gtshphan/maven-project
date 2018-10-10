pipeline {
    agent any

    tools {
        maven 'localMaven'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn.exe clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}