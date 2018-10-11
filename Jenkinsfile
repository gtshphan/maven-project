pipeline {
    agent any

    parameters {
        string(name: 'tomcat_staging', defaultValue: 'localhost:8090', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: 'localhost:8091', description: 'Production Server')
    }
    
    triggers {
        pollSCM('* * * * *') // Polling Source Control
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deployments') {
            parallel {
                stage('Deploy to Staging') {
                    steps {
                        bat "copy C:/Program Files (x86)/Jenkins/workspace/FullyAutomateWithJenkinsfile/webapp/target/*.war C:/sw/apache-tomcat-9.0.12-staging/webapps/"
                    }
                }

                stage("Deploy to Production") {
                    steps {
                        bat "copy C:/Program Files (x86)/Jenkins/workspace/FullyAutomateWithJenkinsfile/webapp/target/*.war C:/sw/apache-tomcat-9.0.12-staging/webapps/"
                    }
                }
            }
        }
    }
}