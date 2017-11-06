pipeline {
    agent {
      label 'osx'
    }
    environment {
      MOCHA_FILE = 'junit/test-results.xml'
      MOCHA_REPORTER = 'mocha-junit-reporter'
    }
    stages {
        stage('Bootstrap') {
          steps {
            sh 'script/bootstrap.py --target_arch=x64 --dev'
          }
        }
        stage('Lint') {
          steps {
            sh 'npm run lint'
          }
        }

        stage('Build') {
          steps {
            sh 'mkdir junit'
            sh 'script/build.py -c D'
          }
        }
        stage('Test'){
          steps {
              sh 'script/test.py --ci --rebuild_native_modules'
          }
        }
    }
    post {
      always {
          junit 'junit/test-results.xml'
      }
    }
}
