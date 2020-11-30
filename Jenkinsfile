pipeline {
    agent any
    stages {
        stage ('Configuring docker agent') {
            agent {
                docker {
                    image 'openjdk:8-jdk-alpine'
                    reuseNode true
                }
            }
        }
        stage ('Checkout & Clone repository') {
            steps {
                git 'https://github.com/diego-yarleque/spring-boot-hello-world-jenkins-ci.git'
            }
        }
        stage ('Build Artifact') {
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