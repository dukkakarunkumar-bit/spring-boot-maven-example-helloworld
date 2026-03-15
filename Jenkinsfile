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

       stage('Checkout') {
    steps {
        git branch: 'master', url: 'https://github.com/dukkakarunkumar-bit/spring-boot-maven-example-helloworld.git'
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
        sh '''
            echo "=== CURRENT DIR ==="
            pwd
            echo "=== FILES ==="
            ls -la
            echo "=== JAVA ==="
            java -version
            echo "=== MAVEN ==="
            mvn -version
            echo "=== BUILD START ==="
            mvn clean package -DskipTests -e
        '''
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
        sh '''
            echo "TOMCAT_WEBAPPS=$TOMCAT_WEBAPPS"
            ls -lh target
            cp -v target/*.war $TOMCAT_WEBAPPS/ROOT.war
        '''
    }
}
    }
}
