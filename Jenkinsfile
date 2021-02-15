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
                withDockerRegistry([credentialsId: 'gitlab-registry', url:'http://10.250.10.2:5050']) {
                    //sh 'docker tag hello-brunch:latest 10.250.10.2:5050/root/hello-brunch-gitlab:latest'
                    //sh 'docker push 10.250.10.2:5050/root/hello-brunch-gitlab:latest'
                    sh 'docker tag hello-brunch:latest 10.250.10.2:5050/root/hello-brunch-gitlab:BUILD-1.${BUILD_NUMBER}'
                    sh 'docker push 10.250.10.2:5050/root/hello-brunch-gitlab:BUILD-1.${BUILD_NUMBER}'
                    sshagent (credentials: ['gitlab-ssh']) {
                        sh 'git tag BUILD-1.${BUILD_NUMBER}'
                        sh 'git push --tags'
                    }                    
                }
            }
        }
    }
}

