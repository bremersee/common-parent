pipeline {
  agent {
    label 'maven'
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Deploy') {
      when {
        anyOf {
          branch 'develop'
        }
      }
      steps {
        sh 'mvn -P deploy deploy'
      }
    }
    stage('Deploy Release') {
      when {
        anyOf {
          branch 'master'
        }
      }
      steps {
        sh 'mvn -P deploy,release deploy'
      }
    }
    stage('Site') {
      when {
        anyOf {
          branch 'develop'
          branch 'master'
        }
      }
      steps {
        sh 'mvn site-deploy'
      }
    }
  }
}