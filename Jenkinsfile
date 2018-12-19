pipeline {
  agent { label 'mfw' }

  environment {
    lib = 'musl'
    startClean = '0'
    makeOptions = '-j32'
  }

  stages {
    stage('Build') {
      parallel {
        stage('Build x86_64') {
          environment {
            device = 'x86_64'
          }
          steps {
            buildMFW($device, $lib, $startClean, $makeOptions)
          }
        }

        stage('Build wrt1900') {
          environment {
            device = 'wrt1900'
          }
          steps {
            buildMFW($device, $lib, $startClean, $makeOptions)
          }
        }

        stage('Build wrt3200') {
          environment {
            device = 'wrt3200'
          }
          steps {
            buildMFW($device, $lib, $startClean, $makeOptions)
          }
        }

        stage('Build omnia') {
          environment {
            device = 'omnia'
          }
          steps {
            buildMFW($device, $lib, $startClean, $makeOptions)
          }
        }

      }
    }
  }
}

def buildMFW(String device, String lib, String startClean, String makeOptions) {
  sh 'docker-compose -f mfw/docker-compose.build.yml -p mfw_${device} run build -d ${device} -l ${lib} -c ${startClean} -m "${makeOptions}"'
}
