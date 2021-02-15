#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Build') {
            steps {
                 git url: 'http://10.250.10.2:8929/root/hello-brunch-gitlab.git', branch: 'publish'
                sh 'docker-compose build'
            }
        }
        stage('Publish') {
            steps {
                withDockerRegistry([credentialsId: 'gitlab-registry', url:'http://10.20.10.2:5050']) {
                    //cont.push()
                    //cont.push('latest')
                }
            }
        }
    }
}

