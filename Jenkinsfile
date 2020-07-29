pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                 git credentialsId: 'git-user', url: 'https://github.com/gauravbhalekar5/web.git'
            }
        }
        stage('Build') {
            steps {
                 sh "mvn clean package"
            }
        } 
        stage('Deploy on Production'){
            steps {
                sshagent(['tomcat-deploy']) {
                    sh """

                    scp -o StrictHostKeyChecking=no target/web.war  ec2-user@54.158.194.65:/opt/tomcat8/webapps

                    ssh root@54.158.194.65 /opt/tomcat8/bin/shutdown.sh

                    ssh root@54.158.194.65 /opt/tomcat8/bin/startup.sh      

                    """
                }
            }
        }     
    }
}
