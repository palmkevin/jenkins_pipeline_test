pipeline {
  agent any
  stages {
    stage('TEST') {
      parallel {
        stage('say hello') {
          steps {
            echo 'Hello from docker'
          }
        }
        stage('get version') {
          steps {
            sh 'python --version'
          }
        }
      }
    }
    stage('say goodby') {
      steps {
        sh '''echo $HOSTNAME
echo good bye'''
      }
    }
  }
}