pipeline {
    agent any

    environment {
        // Define your EC2 instance details
        EC2_INSTANCE_ID = 'i-05af0909d4703bc17'
        EC2_REGION = 'us-east-1'
        TOMCAT_WEBAPP_DIR = '/opt/tomcat/webapps'
        SSH_CREDENTIALS_ID = '1c32d2fa-caee-48c0-a0eb-e34e58ac5782'
    }

    stages {
        stage('Build') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
                
                // Build the Maven project
                sh "mvn clean package"
            }
        }
        stage("Approve Deployment"){
            steps{
                input 'Are you OK with the new changes ?'    
            }
        }
        stage('Deploy to EC2') {
            steps {
                script {
                    // Use the SSH key for deployment
                    withCredentials([sshUserPrivateKey(credentialsId: "${SSH_CREDENTIALS_ID}", keyFileVariable: "SSH_KEY")]) {
                        sh "scp -i $SSH_KEY target/my-maven-webapp.war ec2-user@${EC2_INSTANCE_ID}:${TOMCAT_WEBAPP_DIR}"
                    }
                }
            }
        }
    }
}
