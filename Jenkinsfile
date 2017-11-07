def arches = ['mas', 'osx']
def branches = [:]

for (int i = 0; i < 2 ; i++) {
  def arch = arches[i]
  branches["electron-${arch}-x64"] = {
    stage("electron-${arch}-x64") {
      agent {
        label 'osx'
      }
      steps {
        if (arch === mas) {
          sh 'export MAS_BUILD=1'
        }
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
