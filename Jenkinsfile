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
          bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=cursomc -Dsonar.host.url=http://localhost:9000 -Dsonar.login=03eb81dd19a93ae75ddccb76e48dbf9b2737bb86 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/.mvn/wrapper**,**/src/test/**,**/model/**,**Application.java"
        }
      }
    }
    stage ('Quality Gate') {
      steps {
        sleep(5)
        timeout(time: 1, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}