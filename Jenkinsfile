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

        stage('Deploy') {
            steps {
                // Especificamos la rama que en github ahora es main, no master
                sh 'docker-compose up -d'
            }
        }

        stage('Trivy') {
            steps {
                sh 'trivy image --format json --output trivy-results-hello-brunch.json hello-brunch:latest'
            }
            post {
                always {
                    recordIssues enabledForFailure: true, tool: trivy(pattern: '*.json')
                }
            }
        }  

    }
}
