pipeline {
    agent any
    stages {
        stage('continuous-download') {
            steps {
                git url: 'https://github.com/rchidana/calcwebapp.git'
                branch: 'master'
            }
        }
        
        stage('continuous-build') {
            steps {
                sh 'mvn package'
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
