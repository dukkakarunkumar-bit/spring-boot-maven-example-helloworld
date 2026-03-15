pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS = '/opt/tomcat/webapps'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/dukkakarunkumar-bit/spring-boot-maven-example-helloworld.git'
            }
        }

        stage('Verify Tools') {
            steps {
                sh '''
                    java -version
                    mvn -version
                '''
            }
        }

        stage('Build WAR') {
            steps {
                sh '''
                    pwd
                    ls -la
                    mvn clean package -DskipTests -B
                '''
            }
        }

        stage('Check WAR') {
            steps {
                sh 'ls -lh target/*.war'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'cp -v target/*.war $TOMCAT_WEBAPPS/ROOT.war'
            }
        }
    }
}
