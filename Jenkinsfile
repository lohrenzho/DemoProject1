pipeline {
    agent any

environment {
        GIT_URL = 'https://github.com/lohrenzho/DemoProject1.git'
        TOMCAT_URL = 'http://18.191.85.192:8080/'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git "${GIT_URL}"
            }
        }
        stage("SonarQube analysis") {
            steps {
              withSonarQubeEnv('SonarQ') {
                sh 'mvn -f SampleWebApp/pom.xml clean package sonar:sonar'
              }
            }
          }
         stage('Build with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
         stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: "${TOMCAT_URL}")], contextPath: 'myapp', war: '**/*.war'
            }
        }
    }
}
