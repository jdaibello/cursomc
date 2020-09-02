pipeline {
  agent any
  stages {
    stage ('Build Backend') {
      steps {
        bat 'mvn clean package -DskipTests=true'
      }
    }
    stage ('Unit Tests') {
      steps{
        bat 'mvn test'
      }                
    }
    stage ('Sonar Analysis') {
      environment {
          scannerHome = tool 'SONAR_SCANNER'
      }
      steps {
        withSonarQubeEnv('SONAR_LOCAL') {
          bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=cursomc -Dsonar.host.url=http://localhost:9000 -Dsonar.login=8d36488ac6fa92b810860f84bf7827162e932dc5 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/.mvn/wrapper**,**/src/test/**,**/model/**,**Application.java"
        }
      }
    }
  }
}