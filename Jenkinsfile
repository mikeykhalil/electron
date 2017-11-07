pipeline {
    agent none
    stages {
        stage('Parallel builds') {
            parallel {
                stage('electron-osx-x64') {
                    agent {
                      label 'osx'
                    }
                    steps {
                        sh 'env | sort'
                    }
                }
                stage('electron-mas-x64') {
                    agent {
                        label 'osx'
                    }
                    environment {
                        MAS_BUILD = '1'
                    }
                    steps {
                        sh 'env | sort'
                    }
                }
            }
        }
    }
}
