pipeline {
  agent {
    node {
      label 'lsdev01'
    }
    
  }
  stages {
    stage('activate LS npm repository') {
      steps {
        sh 'exec nrm use labsolution'
      }
    }
    stage('npm install') {
      parallel {
        stage('npm install') {
          steps {
            sh 'npm install'
          }
        }
        stage('') {
          steps {
            input(message: '1, 2 oder 3_', id: '123', ok: 'zes')
          }
        }
      }
    }
    stage('ng build (prod)') {
      steps {
        sh '''cd $LSHOME/web
exec ng build --op $LSHOME/local/web_build --no-progress --prod'''
      }
    }
  }
  environment {
    LSHOME = '/opt/ls/lx/release/kpa'
  }
}