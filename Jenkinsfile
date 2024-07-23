pipeline {
    agent any

    stages {
        
          stage('git checkout') {
                steps {
                    git branch: 'main', url: 'https://github.com/javahometech/ai-leads/'
                }
            }
            stage('maven build'){
                steps{
                    sh 'mvn clean package'
                }
            }
            stage('deplyo'){
                steps{
                    sshagent(['tomcat']) {
                     sh "scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.44.36:/opt/tomcat9/webapps"
                     sh "ssh ec2-user@172.31.44.36 /opt/tomcat9/bin/shutdown.sh"
                      sh "ssh ec2-user@172.31.44.36 /opt/tomcat9/bin/startup.sh"
                    }
                }
            }
    }
}
