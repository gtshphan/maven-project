pipeline {
    agent any

    parameters {
        string(name: 'tomcat_staging', defaultValue: 'localhost', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
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
                        bat "cp **/target/*.war C:\sw\apache-tomcat-9.0.12-staging\webapps\"
                    }
                }

                stage("Deploy to Production") {
                    steps {
                        bat "cp **/target/*.war C:\sw\apache-tomcat-9.0.12-staging\webapps\"
                    }
                }
            }
        }
    }
}