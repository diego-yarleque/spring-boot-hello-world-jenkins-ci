pipeline {
    agent any
    stages {
        stage ('Checkout & Clone repository') {
            steps {
                checkout scm
            }
        }
        stage ('Build Artifact') {
            agent {
                docker {
                    image 'openjdk:8-jdk-alpine'
                    reuseNode true
                }
            }
            steps {
                sh './gradlew clean build'
            }
        }
        stage ('Build & Push docker image') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub', url: 'https://index.docker.io/v1/') {
                    sh 'docker push dryloayza/code-challenge:latest'
                }
            }
        }
    }
}