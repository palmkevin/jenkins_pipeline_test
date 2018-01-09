pipeline {
  agent {
    node {
      label 'lsdev01'
    }
    
  }
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
        stage('show variables') {
          steps {
            sh 'set'
          }
        }
        stage('kpa web build') {
          steps {
            sh '''. initLXEnv.sh kpa
web_ui_build.sh'''
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