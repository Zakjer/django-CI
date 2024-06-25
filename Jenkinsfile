pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Zakjer/django-CI.git'
            }
        }

        stage('Build docker image') {
            steps {
                script {
                        sh 'docker build -t my-app .'
                }
            }
        }

        stage('Push image to DockerHub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u zakjer2003 -p $dockerhubpwd'
                        sh 'docker tag my-app:latest zakjer2003/my-app:django-test'
                        sh 'docker push zakjer2003/my-app:django-test'
                    }
                }
            }
        }
    }
}
