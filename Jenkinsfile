pipeline{
    agent any

    tools {
         maven 'maven'
         jdk 'java'
    }

    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/sreenivas449/java-hello-world-with-maven.git']]])
            }
        }
        
        stage('Sonarqube') {
        environment {
                    scannerHome = tool 'sonar-scanner'
                             }                                                  
                steps {
                        withSonarQubeEnv('sonarqube') {
                        sh "${scannerHome}/bin/sonar-scanner \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://35.203.128.237:9000 \
                    -Dsonar.sources=. \
                    -Dsonar.sourceEncoding=UTF-8" \
                    -Dsonar.projectKey=demo 
                    
                        }
                }
                }   
        stage('build'){
            steps{
               bat 'mvn package'
            }
        }
    }
}
