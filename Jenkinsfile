pipeline {
  agent {
    label 'maven'
  }
  tools {
    jdk 'jdk8'
    maven 'm3'
  }
  stages {
    stage('Tools') {
      steps {
        sh 'java -version'
        sh 'mvn -B --version'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B clean install'
      }
    }
    stage('Deploy') {
      when {
        anyOf {
          branch '1.1.develop'
          branch '1.1.master'
        }
      }
      steps {
        sh 'mvn -B -P deploy clean deploy'
      }
    }
    stage('Site') {
      when {
        anyOf {
          branch '1.1.develop'
          branch '1.1.master'
        }
      }
      steps {
        sh 'mvn -B site-deploy'
      }
    }
  }
}