pipeline{
    agent any
    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/munikrishna22/ai-leads'
            }
        }
         stage("Maven Build"){
            steps{
                sh 'mvn clean package'
            }
        }
         stage("Tomcat Deploy-Dev"){
            steps{
                sshagent(['tomcat-dev']) {
                    // copy war file to tomcat
                sh "scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.43.216:/opt/tomcat9/webapps"
                sh "ssh ec2-user@172.31.43.216 /opt/tomcat9/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.43.216 /opt/tomcat9/bin/startup.sh"
                    
                }
            }
        }
    }
}
