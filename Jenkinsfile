pipeline {
    agent {
      label 'osx'
    }
    stages {
        stage('PreBuild') {
          steps {
            checkout([$class: 'GitSCM', branches: [[name: '**']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'git@github.com:electron/electron.git']]])
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
            sh 'script/build.py -c D'
          }
        }
        stage('Test'){
          steps {
              sh 'script/test.py --ci --rebuild_native_modules'
          }
        }
    }
}
