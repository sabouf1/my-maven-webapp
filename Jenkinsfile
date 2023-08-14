pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                checkout scm
                sh "mvn clean package"
            }
        }

        stage('Deploy to EC2') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'fa5f5f3e-9f3b-40b0-9d27-2d525b917287', path: '', url: 'http://18.212.233.5:8080/')], contextPath: 'my-maven-webapp', war: '**/*.war'
            }
        }
    }
}
