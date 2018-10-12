pipeline {
    agent any

    parameters {
        string(name: 'tomcat_staging', defaultValue: '18.234.94.9', description: 'Staging Server')
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
                        bat "C:\\Windows\\WinSxS\\amd64_openssh-common-components-onecore_31bf3856ad364e35_10.0.17134.1_none_a227092418e9be66\\scp -i C:\\Users\\Hung\\Desktop\\gts\\keys\\udemy-class.pem C:\\Users\\Hung\\Desktop\\gts\\keys\\webapp.war ec2-user@${params.tomcat_staging}:/var/lib/tomcat/webapps"
                    }
                }

//                stage("Deploy to Production") {
//                    steps {
//                        bat "copy C:\\Program Files (x86)\\Jenkins\\workspace\\FullyAutomateWithJenkinsfile\\webapp\\target\\webapp.war  C:\\sw\\apache-tomcat-9.0.12-staging\\webapps\\"
//                    }
//                }
            }
        }
    }
}