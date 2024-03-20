pipeline
{
    agent any
    stages
    {
        stage ('contDownload')
        {
            steps
            {
                git 'https://github.com/SantoshAdurthi/maven.git'
            }
        }
        stage ('contBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage ('contDeployemnet')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '88e9e5f9-c99b-46a4-ad9c-8529726bcbe8', path: '', url: 'http://172.31.10.57:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage ('contTesting')
        {
            steps
            {
                git 'https://github.com/SantoshAdurthi/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline1/testing.jar'
            }
        }
        stage ('contDelivery')
        {
            steps
            {
                input message: 'Need approval from Delivery Manager', submitter: 'sebastien'
                deploy adapters: [tomcat9(credentialsId: '88e9e5f9-c99b-46a4-ad9c-8529726bcbe8', path: '', url: 'http://172.31.1.39:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
