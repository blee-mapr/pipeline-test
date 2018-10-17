pipeline {
  agent any
  stages {
    stage('build') {
      parallel {
        stage('Build base') {
          agent any
          steps {
            sh '''#!/bin/bash
            git diff --name-only HEAD^ HEAD'''
          }
        }
        stage('build something else') {
          agent any
          steps {
            List fileList = getChangedFilesList()
            echo(fileList)
          }
        }
      }
    }
  }
}

def getChangedFilesList() {
  return sh(returnStdout: true, script: 'git diff --name-only HEAD^ HEAD')
}
