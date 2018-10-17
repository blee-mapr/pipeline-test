pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''#!/bin/bash
git diff --name-only HEAD^ HEAD
'''
      }
    }
  }
}