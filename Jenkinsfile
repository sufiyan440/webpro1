currentBuild.displayName = "onlineshopping-#"+currentBuild.number

pipeline {
    agent any
    environment {
    PATH = "/usr/share/maven/bin:$PATH"
    }
    stages {
        stage('Git checkout') {
            steps {
                git credentialsId: 'Gitcrd', url: 'https://github.com/sufiyan440/webpro1.git'
            }
        }
       stage('Maven Build') { 
        steps {
            sh "mvn clean package"
            sh"mv target/*.war target/myweb.war"
            }
        }
        stage('deploy-dev'){
            steps {
        sshagent(['tomcat']) {
           sh""""
           scp -o StrictHostKeyChecking=no target/myweb.war ubuntu@65.2.124.165:/tomcat8/webapps/
           ssh ubuntu@65.2.124.165 /opt/tomcat8/bin/shutdown.sh
           ssh ubuntu@65.2.124.165 /opt/tomcat8/bin/startup.sh
           
           """
                 }
            }
        }             
    }
}
