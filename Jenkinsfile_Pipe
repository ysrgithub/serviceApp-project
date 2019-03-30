pipeline {
    agent any
    tools{
    maven 'Maven3.5.4'
    jdk 'Jdk1.8'
     }
     // using the Timestamper plugin we can add timestamps to the console log
    options {
        timestamps()
        buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '3', numToKeepStr: '3'))
        }
    stages {
      stage ('Initialize Devops Tools') {
                steps {
                sh '''
                    echo "This Jenkinsfile for Building Shopizer Project"
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                    echo "JAVA_HOME = ${JAVA_HOME}"
                    '''
                }
            }
        stage (' Cloning Code base from GIT'){
            steps {
            checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '79d43e10-ce5b-4b14-93a0-7366ee201cbe', url: 'https://github.com/ITHelp-Stream/serviceApp.git']]]
        }
        }
        stage ('Build the code using Maven') {
                steps {
                    sh 'mvn clean compile install'
                    }
         }
        stage ('archiveArtifacts for Shopizer'){
            steps {
                archiveArtifacts '**/**/shopizer.war'
            }
        }
        
    }
}//pipeline
