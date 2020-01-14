pipeline {
    agent any
	environment {
     def mvnHome = tool 'mvn3'
		def JAVA_HOME= tool 'jdk13' 
		def sonarHome=tool 'sonars'
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
		    withEnv(["JAVA_HOME=${ tool 'jdk13' }", "PATH+MAVEN=${tool 'mvn3'}/bin:${env.JAVA_HOME}/bin"]) {
		        		 bat(/"%MVN_HOME%\bin\mvn.cmd" -Dmaven.test.failure.ignore clean compile/)

		    }
                          }
        }
        stage('Test') {
            steps {
                echo 'Testing'
		    withEnv(["JAVA_HOME=${ tool 'jdk13' }", "PATH+MAVEN=${tool 'mvn3'}/bin:${env.JAVA_HOME}/bin"]) {
                 bat(/"%MVN_HOME%\bin\mvn.cmd" -Dmaven.test.failure.ignore test/)
            }
	    }
        }
        stage('Sonar') {
            steps {
                echo 'Sonar Scanner'
               //def scannerHome = tool 'sonar'
			    withSonarQubeEnv('sonar') {	 	
				  //  bat(/"%sonarHome%\bin\sonar-runner.bat"/)
                      // sh './mvnw sonar:sonar -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.login=${SONAR_AUTH_TOKEN}' 
				    bat(/"%MVN_HOME%\bin\mvn.cmd" sonar:sonar /)
        }
        }
        }
      
        stage('Deploy') {
            steps {
                echo '## TODO DEPLOYMENT ##'
		    withEnv(["JAVA_HOME=${ tool 'jdk13' }", "PATH+MAVEN=${tool 'mvn3'}/bin:${env.JAVA_HOME}/bin"]) {
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
}
