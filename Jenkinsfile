pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven'
    }

    environment {
        TOMCAT_WEBAPPS = '/var/lib/tomcat10/webapps'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/syoganandh/spring-boot-maven-example-helloworld.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'cp target/*.war $TOMCAT_WEBAPPS/ROOT.war'
            }
        }
    }
}
