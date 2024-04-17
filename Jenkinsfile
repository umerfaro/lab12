pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/umerfaro/lab12.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-app .'
            }
        }

        stage('Run Docker Image') {
            steps {
                bat 'docker run -d --name my-app-instance my-app'
            }
        }
        stage('Tag docker image') {
            steps {
                bat 'docker tag my-app umer12314sr/my-app'
            }
        }   

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push umer12314sr/my-app'
                }
            }
        }
    }
}