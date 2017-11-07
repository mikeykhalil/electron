def buildarches = [:]

buildarches['electron-osx-x64'] = {
  stage ('electron-osx-x64'){
    node('osx') {
      sh 'echo $MAS_BUILD'
      sh 'script/bootstrap.py --target_arch=x64 --dev'
      sh 'npm run lint'
      sh 'script/build.py -c D'
      sh 'script/test.py --ci --rebuild_native_modules'
    }
  }
}

buildarches['electron-mas-x64'] = {
  stage ('electron-mas-x64'){
    environment {
      MAS_BUILD = '1'
    }
    node('osx') {
      sh 'echo $MAS_BUILD'
      sh 'script/bootstrap.py --target_arch=x64 --dev'
      sh 'npm run lint'
      sh 'script/build.py -c D'
      sh 'script/test.py --ci --rebuild_native_modules'
    }
  }
}

parallel buildarches
