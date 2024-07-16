pipeline{
    agent any
    stages{
        stage("code checkout"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/mahesh0401/ai-leads'
            }
        }
        stage("Maven build"){
            steps{
                sh 'mvn clean package'
            }
        }
            stage("Tomat-dev"){
            steps{
               sshagent(['tomcat-dev']) {
               sh "scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.32.106:/opt/tomcat10/webapps"
               sh "ssh ec2-user@172.31.32.106 /opt/tomcat10/bin/shutdown.sh"
               sh "ssh ec2-user@172.31.32.106 /opt/tomcat10/bin/startup.sh"
                  }
            }
            }
        }
    }

