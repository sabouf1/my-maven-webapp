pipeline {
    agent any

    environment {
        // Define your Elastic Beanstalk application and environment details
        AWS_EB_REGION = 'us-east-1'
        AWS_EB_APPLICATION_NAME = 'tomcat-webapp'
        AWS_EB_ENVIRONMENT_NAME = 'Tomcat-webapp-env'
    }

    stages {
        // ...
        stage('Deploy to Elastic Beanstalk') {
            steps {
                // Use the Elastic Beanstalk Plugin to deploy the application
                withAWS(region: "${AWS_EB_REGION}", credentials: 'aws1') {
                    elasticBeanstalkDeploy(applicationName: "${AWS_EB_APPLICATION_NAME}", environmentName: "${AWS_EB_ENVIRONMENT_NAME}", versionLabel: "v_${BUILD_NUMBER}", artifact: 'target/my-maven-webapp.war')
                }
            }
        }
    }
}
