pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-creds', url: 'https://github.com/VeenaVibhasiniPanyam/hiring'
            }
        }
        stage('Maven Build'){
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat deploy'){
            steps {
                sshagent(['tomcat-creds']) {
                  sh "scp -o StrictHostKeyChecking=no  target/*.war ec2-user@172.31.21.162:/opt/tomcat9/webapps"
                  sh "ssh ec2-user@172.31.21.162 /opt/tomcat9/bin/shutdown.sh"
                  sh "ssh ec2-user@172.31.21.162 /opt/tomcat9/bin/startup.sh"
    
              }
                
            }
    }
}
}
