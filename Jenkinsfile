
def arches = ["mas", "osx"]
def branches = [:]

for (int i = 0; i < 2 ; i++) {
  def arch = arches[i]
  stage ("electron-${arch}-x64") {
    if (arch == 'mas') {
      environment {
        MAS_BUILD = '1'
      }
    }
    branches["electron-${arch}-x64"] = {
      node ('osx') {
        sh 'echo $MAS_BUILD'
        sh 'script/bootstrap.py --target_arch=x64 --dev'
        sh 'npm run lint'
        sh 'script/build.py -c D'
        sh 'script/test.py --ci --rebuild_native_modules'
      }
    }
  }
}

parallel branches
