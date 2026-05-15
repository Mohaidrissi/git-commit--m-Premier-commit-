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

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        bat 'docker login -u %DOCKERHUB_USERNAME% -p %DOCKERHUB_PASSWORD%'
                        bat 'docker tag %IMAGE_NAME% %DOCKERHUB_USERNAME%/%IMAGE_NAME%:latest'
                        bat 'docker push %DOCKERHUB_USERNAME%/%IMAGE_NAME%:latest'
                    }
                }
            }
        }
    }






}