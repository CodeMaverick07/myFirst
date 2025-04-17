pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    environment {
        TOMCAT_URL = 'http://localhost:9090/manager/text'
        TOMCAT_CREDENTIALS = 'tomcat-cred'
    }
    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/codemaverick07/myfirst.git'
            }
        }
        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: "${TOMCAT_CREDENTIALS}", url: "${TOMCAT_URL}")], contextPath: 'myfirst', war: 'target/myfirst.war'
            }
        }
    }
}