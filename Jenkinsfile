#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Trivy') {
            steps {
                sh 'trivy filesystem --format json --output trivy-results-filesystem.json .'
                sh 'trivy image --format json --output trivy-results-hello-brunch.json hello-brunch:latest'
            }
            post {
                always {
                    recordIssues enabledForFailure: true, aggregatingResults: true, tool: trivy(pattern: '*.json')
                }
            }
        }  

        stage('Deploy') {
            steps {
                // Especificamos la rama que en github ahora es main, no master
                sh 'docker-compose up -d'
            }
        }        

    }
}
