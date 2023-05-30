pipeline {
   agent any
    stages {
        stage('continuous-download') {
            steps {
             git 'https://github.com/rchidana/calcwebapp.git'
            }
        }
        stage('sonarqube'){
            steps{
                withSonarQubeEnv('sonar-qube') {
                  sh 'mvn package sonar:sonar'
                }
            }
        }
        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "jfrog_143",
                    releaseRepo: 'venu-libs-release-local',
                     snapshotRepo: 'venu-libs-snapshot-local'
                ) 
            }
        } 
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'maven3.9.2', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'package',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }         
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "jfrog_143"
                )
            }
        }
    }
}
