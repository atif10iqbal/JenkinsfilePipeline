pipeline
{
    agent any
    stages
    {
        stage('Continuous Download')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('Continuous Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Continuous Deploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '173e4154-7803-4bc8-9b85-13492aaf72b7', path: '', url: 'http://172.31.42.85:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('Continuous Testing')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /root/.jenkins/workspace/DeclrativePipeline-1/testing.jar'
            }
        }
        stage('Continuous Delivery')
        {
            steps
            {
                input message: 'Need approval from DM!', submitter: 'iqbal'
                deploy adapters: [tomcat9(credentialsId: '173e4154-7803-4bc8-9b85-13492aaf72b7', path: '', url: 'http://172.31.42.85:8080')], contextPath: 'app', war: '**/*.war'
            }
        }
        
    }
}
