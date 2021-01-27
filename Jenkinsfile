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
    }
}
