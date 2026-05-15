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

           
         stage('login Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-id',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                  bat '''
                   @echo off
                   echo %DOCKER_PASS%| docker login -u %DOCKER_USER% --password-stdin
                  '''                }
              }
           }
         stage('Build Docker Image') {
            steps {
                bat ' docker build -t %IMAGE_NAME% . '
            }
        }
         stage('tag Docker Image') {
            steps {
                bat ' docker tag %IMAGE_NAME% mohamedibnmustapha/%IMAGE_NAME%'
            }
        }
         stage('push Docker Image') {
            steps {
                bat ' docker push mohamedibnmustapha/%IMAGE_NAME%'
            }
        }
    }






}