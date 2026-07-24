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
          echo "building the application..."
          sh 'mvn package'
        }
      }
    }
    stage("build image") {
      steps {
        script {
          echo "building the docker image..."
          withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
            sh 'docker build -t analystrusso/twn-bootcamp-repo:jma-2.0 .'
            sh 'echo $PASS | docker login -u $USER --password-stdin'
            sh 'docker push analystrusso/twn-bootcamp-repo:jma-2.0'
          }
        }
      }
    }
    stage("deploy") {
      steps {
        script {
          echo "deploying the application..."
        }
      }
    }
  }
}
