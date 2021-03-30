pipeline {
    agent any

    tools {
        maven 'my-maven' 
    }
    stages {
       stage ('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/zakaria2905/mywebappsecurity.git"
            }

        }
       stage('Build & Unit test'){
          steps {
               sh 'mvn clean package';
               junit '**/target/surefire-reports/TEST-*.xml'
              //    archiveArtifacts  'target/*.jar'
           }
       }
       stage('Security SAST : SonarQube'){
           steps {
                 sh "mvn sonar:sonar  -Dsonar.host.url=http://host.docker.internal:9000  -Dsonar.projectName=mywebappsecurity -Dsonar.projectKey=mywebappsecurity -Dsonar.projectVersion=$BUILD_NUMBER";
           }
        }
    }
}