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
                git 'https://github.com/dukkakarunkumar-bit/spring-boot-maven-example-helloworld.git'
            }
        }

        stage('Verify Tools') {
            steps {
                sh 'java -version'
                sh 'mvn -v'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Check WAR') {
            steps {
                sh 'ls -lh target'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'cp target/*.war $TOMCAT_WEBAPPS/ROOT.war'
            }
        }
    }
}
