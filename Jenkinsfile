
pipeline {
   agent any
   tools{
       jdk 'JDK1.8'
       maven 'Maven3'
   }
   options {
       timestamps()
       cleanWs()
       buildDiscarder(logRotator(artifactDaysToKeepStr: '10', artifactNumToKeepStr: '10', daysToKeepStr: '10', numToKeepStr: '10'))
   }
 stages {
     stage ('Display PATH of Jenkins'){
         steps {
             sh '''
             echo "This is Declarative pipeline for building ServiceApp"
             echo "PATH = ${PATH}"
             '''
         }
     }
     stage ('Checkout the Source Code') {
        steps {
         checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '2d2da1f8-e62f-4fe2-bb86-13b88b0c02e3', url: 'https://github.com/ITHelp-Stream/serviceApp.git']]])
        }
    }
      stage ('Building the Souce using Maven') {
          steps {
              sh 'mvn clean compile install'
          }
      }
      stage ('Archive artifacts for ServiceApp'){
          steps{
              archiveArtifacts '**/**/*.war'
          }
      }
    }
}