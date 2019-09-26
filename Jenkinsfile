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
          branch 'master'
        }
      }
    stage('Snapshot Site') {
      when {
        branch 'develop'
      }
      steps {
        sh 'mvn site-deploy'
      }
    }
    stage('Release Site') {
      when {
        branch 'master'
      }
      steps {
        sh 'mvn -P gh-pages-site site site:stage scm-publish:publish-scm'
      }
    }
      steps {
        sh 'mvn -P deploy deploy'
      }
    }
  }
}