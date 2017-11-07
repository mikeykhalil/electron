def arches = ["mas", "osx"]
def branches = [:]

for (int i = 0; i < 2 ; i++) {
  def arch = arches[i]
  branches["electron-${arch}-x64"] = {
    node ('osx') {
      stages {
        stage('Set MAS build') {
          when { arch 'mas' }
          environment {
            MAS_BUILD = 1
          }
        }
        stage('Bootstrap') {
          steps {
            sh 'echo $MAS_BUILD'
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
  }
}

parallel branches
