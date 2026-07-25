#!/user/bin/env groovy
@Library('jenkins-shared-library@main')
def gv

pipeline {
    agent any
    tools {
        maven 'Maven'
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
                    buildJar()
                }
            }
        }
        stage("build image") {
            steps{
                script{
                    buildImage 'analystrusso/twn-bootcamp-repo:jma-3.0'
                }
            }
        }
        stage("deploy") {
            steps{
                script{
                    gv.deployApp()
                }
            }
        }
    }
}
