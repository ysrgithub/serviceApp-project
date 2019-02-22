pipeline {
    agent any
    tools{
    maven 'M2_HOME'
    jdk 'JDK1.8'
     }
     // using the Timestamper plugin we can add timestamps to the console log
    options {
        timestamps()
        buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5'))
        }
    stages {
        /**stage ('Initialize for Shopizer') {
                steps {
                sh '''
                    echo "This Jenkinsfile for Building Shopizer Project"
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                    echo "JAVA_HOME = ${JAVA_HOME}"
                    '''
                }
            }**/
        stage (' Cloning Code base from GIT'){
            steps {
                checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '58625aea-0548-44b3-9600-627c0f16af02', url: 'https://github.com/ITHelp-Stream/serviceApp.git']]]
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
         stage ('Push Artifacts to Nexus'){
            steps {
                nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'sm-shop/target/shopizer.war']], mavenCoordinate: [artifactId: 'shopizer', groupId: 'com.shopizer', packaging: 'war', version: '2.4.0']]]
            }
        }
        
    }
}//pipeline
