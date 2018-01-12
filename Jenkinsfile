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
      steps {
        sh 'npm install'
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