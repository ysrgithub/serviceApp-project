pipeline{
 agent any
 tools{
 maven 'Maven3.5.4'
 jdk 'Jdk1.8'
 }
options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5'))
}
stages{
	stage('Checkout Source Code'){
	steps{
	print "cloning  Source Code from GitHub repository"
	checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '79d43e10-ce5b-4b14-93a0-7366ee201cbe', url: 'https://github.com/ITHelp-Stream/serviceApp.git']]]
		}
	}
	stage('Building Code using Maven'){
	steps{
	sh 'mvn clean compile install'	
	}
	}
	stage('Archive the Artifacts'){
	steps{
	archiveArtifacts '**/**/*.war'
	}
	}

	}//stages
}//pipeline
