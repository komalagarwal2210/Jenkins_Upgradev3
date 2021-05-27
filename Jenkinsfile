pipeline {
    agent any
     tools {

        maven 'LocalMaven'

        jdk 'LocalJava'

    }
    stages {
        stage('Build Application') {
            steps {
                bash 'mvn -f java-tomcat-sample/pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
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

