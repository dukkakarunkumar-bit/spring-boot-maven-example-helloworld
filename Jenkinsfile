pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS = '/var/lib/tomcat10/webapps'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/dukkakarunkumar-bit/spring-boot-maven-example-helloworld.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh '''
                    java -version
                    mvn -version
                    mvn clean package -DskipTests -B
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'sudo cp -v target/*.war $TOMCAT_WEBAPPS/ROOT.war'
            }
        }
    }
}
