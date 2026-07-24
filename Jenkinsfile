// This file will build the java app, build the docker image, and then push them to a private repo.

def gv

pipeline {
  agent any
  tools {
    maven 'maven-3.9'
  }
  stages {
    stage("init") {
          steps {
            script {
              gv = load "script.groovy"
            }
          }
    }
    stage("build jar") {
      steps {
        script {
          gv.buildJar()
        }
      }
    }
    stage("build image") {
      steps {
        script {
          gv.buildImage()
        }
      }
    }
    stage("deploy") {
      steps {
        script {
          gv.deployApp()
        }
      }
    }
  }
}
