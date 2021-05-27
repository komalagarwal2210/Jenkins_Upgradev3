pipeline {
      agent any
      stages {
            
            stage('Build') {
                  steps {
                        sh 'mvn -f java-tomcat-sample/pom.xml clean package'
                  }
		  post {
		    success{
		  	echo "Now archiving the artifacts"
			archiveArtifacts artifacts: '**/*.war'
		  }
		}

            }
            stage('Deploy') {
                  steps {
                        build job: 'DeployApplication'
                  }
            }
            stage('Deploy Production') {
                  steps {
                        echo "Deploying in Production Area"
                  }
            }
      }
}
