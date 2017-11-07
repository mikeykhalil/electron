pipeline {
    agent any
    stages {
        stage('Parallel builds') {
            parallel {
                stage('electron-osx-x64') {
                    steps {
                        echo "electron-osx-x64 "
                    }
                }
                stage('electron-mas-x64') {
                    steps {
                        echo "electron-mas-x64"
                    }
                }
            }
        }
    }
}
