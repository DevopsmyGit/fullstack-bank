pipeline {
    agent any
    
    tools{
        jdk 'jdk11'
        nodejs 'nodejs17'
        maven 'maven3'
        
    }
    
    
    
    stages {
        stage('SCM'){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/DevopsmyGit/spring-proj.git'
            }
        }

        stage('Static Code Analysis') {
          environment {
            SONAR_URL = "http://192.168.64.1:9000/"
          }
          steps {
            withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
              sh 'mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
            }
          }
        }
        
        
         stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        
        stage('Backend') {
            steps {
                dir('/root/.jenkins/workspace/Bank/app/backend') {
                    sh "npm install"
                }
            }
        }
        
        stage('frontend') {
            steps {
                dir('/root/.jenkins/workspace/Bank/app/frontend') {
                    sh "npm install"
                }
            }
        }
    }
}
