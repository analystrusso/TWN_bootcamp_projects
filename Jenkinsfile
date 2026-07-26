#!/user/bin/env groovy

@Library('jenkins-shared-library@main', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/analystrusso/jenkins-shared-library.git',
    credentialsId: 'github-creds])
     
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
                    buildImage 'analystrusso/twn-bootcamp-repo:jma-3.1'
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
