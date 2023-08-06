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
                deploy adapters: [tomcat8(credentialsId: 'fa5f5f3e-9f3b-40b0-9d27-2d525b917287', path: '', url: 'http://34.202.165.13:8080/')], contextPath: 'my-maven-webapp', war: '**/*.war'
            }
        }
    }
}
