pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout'
            }
        }
        stage('Build') {
            steps {
                echo 'Clean Build'
                bat 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                bat 'mvn test'
            }
        }
        stage('JaCoCo') {
		step{[$class: 'JacocoPublisher', 
      execPattern: 'target/*.exec',
      classPattern: 'target/classes',
      sourcePattern: 'src/main/java',
      exclusionPattern: 'src/test*'
		     ]}
	}
        stage('Sonar') {
            steps {
                echo 'Sonar Scanner'
               	//def scannerHome = tool 'SonarQube Scanner 3.0'
			    withSonarQubeEnv('SonarQube Server') {
			    	bat 'C:/Users/sindu.mary.lawrence/Downloads/sonar-runner-dist-2.4/sonar-runner-2.4/bin/sonar-runner'
			    }
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging'
                bat 'mvn package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
                echo '## TODO DEPLOYMENT ##'
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
