pipeline {
    agent {
      label 'osx'
    }
    stages {
        stage('PreBuild') {
          steps {
            checkout([$class: 'GitSCM', branches: [[name: '**']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'git@github.com:electron/electron.git']]])
            script/bootstrap.py --target_arch=x64 --dev
          }
        }
        stage('Lint') {
          steps {
            npm run lint
          }
        }

        stage('Build') {
          steps {
            script/build.py -c D
          }
        }
        stage('Test'){
          steps {
              script/test.py --ci --rebuild_native_modules
          }
        }
    }
}
