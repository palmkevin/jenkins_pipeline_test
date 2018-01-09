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
# web_ui_build.sh'''
          }
        }
        stage('UT') {
          steps {
            sh '''exit 0

. /etc/profile
. ~/.profile
. initLXEnv.sh BUILD_PERMANENT
export PYTHONPATH=$LSHOME:$LSHOME/python32/ls/tests:$PYTHONPATH

# 0. lxs
echo -e "[junit-xml]\\npath = lxs-junit.xml" > junit.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config junit.cfg --junit-xml nose2helper lxs.tests 

# 1. ls.smb.pricing.ac
echo -e "[junit-xml]\\npath = ls.smb.pricing.ac-junit.xml" > junit.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config junit.cfg --junit-xml nose2helper ls.smb.tests.pricing.ac 

# 2. ls.smb.transform
echo -e "[junit-xml]\\npath = ls.smb.transform-junit.xml" > junit.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config junit.cfg --junit-xml ls.smb.tests.transform.cases 

# 3. itf.highlevel
echo -e "[junit-xml]\\npath = itf.highlevel-junit.xml" > junit.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config junit.cfg --junit-xml nose2helper itf.highlevel.tests 

# 4. ls.tools.importer
echo -e "[junit-xml]\\npath = ls.tools.importer-junit.xml" > junit.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config junit.cfg --junit-xml nose2helper ls.tools.importer.tests
'''
          }
        }
      }
    }
    stage('run unit tests') {
      parallel {
        stage('LXS') {
          steps {
            sh '''
. /etc/profile
. ~/.profile
. initLXEnv.sh BUILD_PERMANENT
export PYTHONPATH=$LSHOME:$LSHOME/python32/ls/tests:$PYTHONPATH

export JUNIT_NAME=lxs

echo -e "[junit-xml]\\npath = $JUNIT_NAME-junit.xml" > $JUNIT_NAME.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config $JUNIT_NAME.cfg --junit-xml nose2helper lxs.tests 
'''
          }
        }
        stage('ITF') {
          steps {
            sh '''#exit 0

#. /etc/profile
#. ~/.profile
#. initLXEnv.sh BUILD_PERMANENT
#export PYTHONPATH=$LSHOME:$LSHOME/python32/ls/tests:$PYTHONPATH

export JUNIT_NAME=itf.highlevel

echo -e "[junit-xml]\\npath = $JUNIT_NAME-junit.xml" > $JUNIT_NAME.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config $JUNIT_NAME.cfg --junit-xml nose2helper itf.highlevel.tests 
'''
          }
        }
        stage('ls.smb.transform') {
          steps {
            sh '''exit 0

. /etc/profile
. ~/.profile
. initLXEnv.sh BUILD_PERMANENT
export PYTHONPATH=$LSHOME:$LSHOME/python32/ls/tests:$PYTHONPATH

export JUNIT_NAME=ls.smb.transform

echo -e "[junit-xml]\\npath = $JUNIT_NAME-junit.xml" > $JUNIT_NAME.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config $JUNIT_NAME.cfg --junit-xml ls.smb.tests.transform.cases 
'''
          }
        }
        stage('ls.smb.pricing.ac') {
          steps {
            sh '''exit 0

. /etc/profile
. ~/.profile
. initLXEnv.sh BUILD_PERMANENT
export PYTHONPATH=$LSHOME:$LSHOME/python32/ls/tests:$PYTHONPATH

export JUNIT_NAME=ls.smb.pricing.ac

echo -e "[junit-xml]\\npath = $JUNIT_NAME-junit.xml" > $JUNIT_NAME.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config $JUNIT_NAME.cfg --junit-xml nose2helper ls.smb.tests.pricing.ac 
'''
          }
        }
        stage('ls.tools.importer') {
          steps {
            sh '''exit 0

. /etc/profile
. ~/.profile
. initLXEnv.sh BUILD_PERMANENT
export PYTHONPATH=$LSHOME:$LSHOME/python32/ls/tests:$PYTHONPATH

export JUNIT_NAME=ls.tools.importer

echo -e "[junit-xml]\\npath = $JUNIT_NAME-junit.xml" > $JUNIT_NAME.cfg
python3 -m nose2 --plugin nose2.plugins.junitxml --config $JUNIT_NAME.cfg --junit-xml nose2helper ls.tools.importer.tests
'''
          }
        }
      }
    }
    stage('Archive test results') {
      steps {
        junit '*-junit.xml'
      }
    }
  }
}