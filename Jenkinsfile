pipeline {
  agent { docker { 
    label 'linux'
    image 'maven:3.5-alpine'
      }
  }
  stages {
    stage ('Checkout') {
      steps {
        git 'https://github.com/CDarnielle/spring-petclinic.git'
      }
    }
    stage ('Build') {
      steps {
        sh 'mvn clean package'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
    stage ('Deploy') {
      steps {
        input 'Do you approve the deployment?'
        echo 'Deploying...'
      }
    }
  }
}
