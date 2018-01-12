pipeline {
  agent {
    node {
      label 'lsdev01'
    }
    
  }
  stages {
    stage('activate LS npm repository') {
      steps {
        sh '''nrm use labsolution
if [ "$?" -ne 0 ]; then exit "$?"; fi'''
      }
    }
    stage('npm install') {
      steps {
        sh '''npm install
if [ "$?" -ne 0 ]; then exit "$?"; fi
'''
      }
    }
    stage('ng build (prod)') {
      steps {
        sh '''exec ng build --op $LSHOME/local/web_build --no-progress --prod
if [ "$?" -ne 0 ]; then exit "$?"; fi
'''
      }
    }
  }
  environment {
    LSHOME = '/opt/ls/lx/release/kpa'
  }
}