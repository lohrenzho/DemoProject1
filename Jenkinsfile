pipeline {
    agent any

environment {
        GIT_URL = 'https://github.com/lohrenzho/DemoProject1.git'
        TOMCAT_URL = 'http://18.222.36.86:8080/'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git "${GIT_URL}"
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
