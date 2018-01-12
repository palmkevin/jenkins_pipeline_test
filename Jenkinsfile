pipeline {
  agent {
    node {
      label 'lsdev01'
    }
    
  }
  stages {
    stage('UT') {
      parallel {
        stage('Update other') {
          steps {
            sh '''# ---------- Update other
/opt/ls/lx/local/ux_bin/ls_deploy.sh updateOther "kpa"
if [ "$?" -ne 0 ]; then exit 1; fi
'''
          }
        }
        stage('update Uniface') {
          steps {
            sh '''/opt/ls/lx/local/ux_bin/ls_deploy.sh updateUniface "kpa"
if [ "$?" -ne 0 ]; then exit 1; fi
'''
          }
        }
      }
    }
    stage('compile uniface') {
      parallel {
        stage('compile uniface') {
          steps {
            echo 'end'
            sh '''# ---------- Compile uniface (nodelete)
/opt/ls/lx/local/ux_bin/ls_deploy.sh unifaceCompile dev "kpa" --noDelete 1
if [ "$?" -ne 0 ]; then exit 1; fi
'''
          }
        }
        stage('web build') {
          steps {
            sh '''# ---------- Web build
. /etc/profile
. ~/.profile
. initLXEnv.sh kpa

web_ui_build.sh
if [ "$?" -ne 0 ]; then exit 1; fi
'''
          }
        }
      }
    }
  }
}