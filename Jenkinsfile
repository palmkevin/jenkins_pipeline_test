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
            sh '''. /etc/profile
. ~/.profile
. initLXEnv.sh kpa
web_ui_build.sh'''
          }
        }
        stage('UT') {
          steps {
            sh '''. /etc/profile
. ~/.profile
. initLXEnv.sh BUILD_PERMANENT
export PYTHONPATH=$LSHOME:$LSHOME/python32/ls/tests:$PYTHONPATH

python3 -m nose2 --plugin nose2.plugins.junitxml --junit-xml nose2helper lxs.tests
exit 0'''
            junit 'nose2-junit.xml'
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