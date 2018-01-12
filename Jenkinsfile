pipeline {
  agent {
    node {
      label 'lsdev01'
    }
    
  }
  stages {
    stage('UT') {
      parallel {
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
        stage('') {
          steps {
            sh 'exit 1'
          }
        }
      }
    }
    stage('') {
      steps {
        echo 'end'
      }
    }
  }
}