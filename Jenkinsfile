buildSteps = {
  sh 'env | sort'
  sh 'script/bootstrap.py --target_arch=x64 --dev'
  sh 'npm run lint'
  sh 'script/build.py -c D'
  sh 'script/test.py --ci --rebuild_native_modules'
}

pipeline {
    agent none
    stages {
        stage('Parallel builds') {
            parallel {
                stage('electron-osx-x64') {
                    agent {
                      label 'osx'
                    }
                    steps buildSteps
                }
                stage('electron-mas-x64') {
                    agent {
                        label 'osx'
                    }
                    environment {
                        MAS_BUILD = '1'
                    }
                    steps buildSteps
                }
            }
        }
    }
}
