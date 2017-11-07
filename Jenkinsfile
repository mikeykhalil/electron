def buildSteps = {
  sh 'env | sort'
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
