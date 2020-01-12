pipeline {
    agent any
	environment {
     def mvnHome = tool 'mvn3'
   }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout'
            }
        }
        stage('Build') {
            steps {
                echo 'Clean Build'
		        		 bat(/"%MVN_HOME%\bin\mvn.cmd" -Dmaven.test.failure.ignore clean compile/)


                          }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                 bat(/"%MVN_HOME%\bin\mvn.cmd" -Dmaven.test.failure.ignore test/)
            }
        }
        stage('Sonar') {
            steps {
                echo 'Sonar Scanner'
               //def scannerHome = tool 'sonar'
			    withSonarQubeEnv('SonarQube Server') {
			    	bat 'C:/Users/sindu.mary.lawrence/Downloads/sonar-runner-dist-2.4/sonar-runner-2.4/bin/sonar-runner'
			    }
            }
        }
        
        stage('Deploy') {
            steps {
                echo '## TODO DEPLOYMENT ##'
		     bat(/"%MVN_HOME%\bin\mvn.cmd" -Dmaven.test.failure.ignore deploy/)
            }
        }
    }
    
    post {
        always {
            echo 'JENKINS PIPELINE'
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
