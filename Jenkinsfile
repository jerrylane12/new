pipeline {
    agent any
    tools {
        maven 'LocalMaven'
    }
    stages{
        stage('Build Maven') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker image build . -t pulkitk567/devops-integration'
                }
            }
        }
        stage('Pushing Docker image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'pulkitk567', variable: 'dockerhubpwd')]) {
                        bat 'docker login -u pulkitk567 -p %dockerhubpwd%'
                        bat 'docker push pulkitk567/devops-integration'
                    }
                }
            }
        }
    }
}
