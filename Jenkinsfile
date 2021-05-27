pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                bat 'mvn -f java-tomcat-sample/pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: 'java-tomcat-sample/target/*.war'
                }
            }
        }
        stage('Deploy in Staging Environment'){
            steps{
                build job: 'DeployApplication'

            }

        }
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                build job: 'DeployApplication'
            }
        }
    }
}

