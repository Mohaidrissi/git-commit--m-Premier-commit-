pipeline {
    agent any
    environment {
        IMAGE_NAME = 'mohamedibnmustapha/mon-app-js:latest'
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
                    sh 'npm install'
                }
            }
        } 

        stage('npm Tests') {
            steps {
                script {
                    sh 'npm test'
                }
            }
        }

           
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }
    }
}