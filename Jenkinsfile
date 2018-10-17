pipeline {
  agent any
  stages {
    stage('get info and set env') {
      steps {
        echo "setting up env"
      }
    }
    stage('build') {
      parallel {
        stage('Build base image') {
          agent any
          steps {
            sh '''#!/bin/bash
            git diff --name-only HEAD^ HEAD'''
          }
        }
        stage('Build all other docker images') {
          agent any
          /*
          steps {
            script {
              env.FILELIST = getChangedFilesList()
            }
            echo "${env.FILELIST}"
          }
          */
          steps {
            script {
              env.FILELIST = getChangedFilesList()
            }
            executeDockerBuild(env.FILELIST)
          }
        }
      }
    }
  }
}

void executeDockerBuild(String fileList) {
  def allModules = ['cldb', 'spark']

  allModules.each { module ->
    script {
      stage(module) {
        echo(fileList)
      }
    }
  }
}

def getChangedFilesList() {
  return sh(returnStdout: true, script: 'git diff --name-only HEAD^ HEAD')
}
