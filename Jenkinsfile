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
    }
}
