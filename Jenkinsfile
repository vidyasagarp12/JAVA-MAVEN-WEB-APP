pipeline{
	agent any
	environment {
	    PATH = "$PATH:/opt/apache-maven-3.9.9/bin"
	}
	stages{
	    stage('Get SCM1 Code'){
	        steps{
			    git branch: 'main', url: 'https://github.com/vidyasagarp12/JAVA-MAVEN-WEB-APP.git'
					}
		}
	    stage('Build'){
		    steps{
			    sh 'mvn clean package'
			}
		}
	    stage('SonarQube analysis') {
			steps{
	            withSonarQubeEnv('SonarQube-v10.7') {
			        sh 'mvn sonar:sonar'
				}
			}
	    }
	    stage('Code Deploy') {
			steps{
	            sshagent(credentials: ['Sagar-SSH-Key']) {
	              sh 'scp -o StrictHostKeyChecking=no target/01-coss-App.war root@192.168.0.196:/opt/apache-tomcat-9.0.97/webapps/'
			}
		 }
	    }
	}
}
