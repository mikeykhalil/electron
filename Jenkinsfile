
def buildsteps = {
    sh 'echo $MAS_BUILD'
    sh 'script/bootstrap.py --target_arch=x64 --dev'
    sh 'npm run lint'
    sh 'script/build.py -c D'
    sh 'script/test.py --ci --rebuild_native_modules'
}

def buildarches = [:]

buildarches['electron-osx-x64'] = {
  stage ('electron-osx-x64'){
    node('osx') {
      steps buildsteps
    }
}

buildarches['electron-mas-x64'] = {
  stage ('electron-mas-x64'){
    node('osx') {
      environment {
        MAS_BUILD = '1'
      }
      steps buildsteps
    }
}

parallel branches
