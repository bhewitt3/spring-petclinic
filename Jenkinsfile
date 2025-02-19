pipeline {
        agent any
          tools {
		maven "Maven"
		jdk "JDK17"
        }
        triggers {
                cron('H/10 * * * 1')
        }
	
	stages {
		stage('Checkout') {
			steps {
				checkout scm
			}
		}
		
		stage('Build') {
			steps {
				sh 'mvn clean verify'
			}
		}
            stage('Generate Report') {
              steps {
                sh 'mvn test jacoco:report'
              }
            }
            stage('Archive jacoco report') {
              steps {
                jacoco execPattern: '**/target/jacoco.exec'
              }
            }
        }
	
	post {
		success {
			echo 'Build Successful'
			archiveArtifacts 'target/*.jar'
		}
		
		failure{
			echo 'Build failed'
		}
	}
}
