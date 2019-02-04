pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: 'localhost', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**\target\*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "winscp -i C:\Program Files (x86)\Jenkins\workspace\Maven-project\webapp\*.war localhost@${params.tomcat_dev}:E:\Tomcat8\apache-tomcat-8.5.37-staging\webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "winscp -i C:\Program Files (x86)\Jenkins\workspace\Maven-project\webapp\*.war localhost@${params.tomcat_prod}:E:\Tomcat8\apache-tomcat-8.5.37-prod\webapps"
                    }
                }
            }
        }
    }
}
