pipeline {
  agent {
    node {
      label 'maven-jdk-8'
    }
    
  }

  stages {
    stage('Preparation') {
      steps {
        git(url: 'https://github.com/jglick/simple-maven-project-with-tests.git', branch: 'master')
        sh 'echo "hello"'
      }
    }
  stage('compile') {
          agent any
          steps {
            sh 'echo \'Perform compilation\''
          }
        }
    stage('Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore clean package'
      }
    }
    stage('test') {
      parallel {
        stage('Result') {
          steps {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
          }
        }
        
      }
    }
  }
}
