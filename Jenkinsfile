pipeline {
  agent any
  stages {
    stage('build') {
      parallel {
        stage('Build base') {
          agent any
          steps {
            sh '''#!/bin/bash git diff --name-only HEAD^ HEAD'''
          }
        }
        stage('build something else') {
          agent any
          steps {
            sh '''echo building something else'''
          }
        }
      }
    }
  }
}
