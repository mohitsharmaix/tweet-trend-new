pipeline {
    agent {label 'maven'}

environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
        stage("build"){
         steps {
            echo "-------------- Build Steps Started -----------"
            sh 'mvn clean deploy -Dmaven.test.skip=true'
            echo "-------------- Build Steps Completed -----------"
         }
    }
        stage("test"){
         steps {
            echo "-------------- unit test Started -----------"
            sh 'mvn surefire-report:report'
            echo "-------------- unit test Completed -----------"
         }
    }
        stage("SonarQube analysis"){
        environment{
            scannerHome = tool 'my-sonar-scanner'
        }
         steps {
         withSonarQubeEnv('my-sonarqube-server'){
            sh "${scannerHome}/bin/sonar-scanner"            
         }
        }         
    }
    }
}
