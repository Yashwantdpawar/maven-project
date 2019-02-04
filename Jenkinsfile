pipeline {
    agent any
    parameters {
        string(name: 'tomcat_dev', defaultValue: 'localhost', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
      stage('Deployments'){
        parallel{
          stage ('Deploy to Staging'){
            steps{
              sh "cp -i C:\Program Files (x86)\Jenkins\workspace\Maven-project\webapp **/target/*.war localhost@${params.tomcat_dev}:E:\Tomcat 8\apache-tomcat-8.5.37-staging\webapps"
            }
        }
          stage ('Deploy to Production'){
            steps{
              sh "cp -i C:\Program Files (x86)\Jenkins\workspace\Maven-project\webapp **/target/*.war localhost@${params.tomcat_dev}:E:\Tomcat 8\apache-tomcat-8.5.37-staging\webapps"
            }
        }
      }
   }
 }
}
