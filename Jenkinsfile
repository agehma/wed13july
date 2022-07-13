pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                
                {
                    try
                    {
                        git 'https://github.com/agehma/wed13july.git'
                    }
                    catch (Exception e1)
                    {
                        mail bcc: '', body: 'git failed to download code from the github', cc: '', from: '', replyTo: '', subject: 'download failed', to: 'gt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch (Exception e2)
                    {
                        mail bcc: '', body: 'mvn failed to build artifact', cc: '', from: '', replyTo: '', subject: 'mvn failed', to: 'devt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.91.123:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch (Exception e3)
                    {
                        mail bcc: '', body: 'deploy to qaserver failed ', cc: '', from: '', replyTo: '', subject: 'deploy to qaserver failed', to: 'mwt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/testingscript1.git'
                        sh 'java -jar /var/lib/jenkins/workspace/DeclarativePE/testing.jar'
                    }
                    catch (Exception e4)
                    {
                        mail bcc: '', body: 'selenium failed to test artifact', cc: '', from: '', replyTo: '', subject: 'selenium failed', to: 'st@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.85.56:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch (Exception e5)
                    {
                        mail bcc: '', body: 'delivery into prodserver tomcat failed', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'delt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
    }
}

