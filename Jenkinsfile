pipeline {
    agent any
    environment {
        IMAGE_NAME = 'mon-app-js'
    }
    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('npm install') {
            steps {
                script {
                    bat 'npm install'
                }
            }
        } 

        stage('npm Tests') {
            steps {
                script {
                    bat 'npm test'
                }
            }
        }

           
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t %IMAGE_NAME% .'
                }
            }
        }
    }
}