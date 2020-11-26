pipeline {
    environment {
        registry = "dryloayza/codechallenge"
        registryCredential = 'dockerhub'
    }
    agent {
        docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            image 'dryloayza/agent:latest'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/diego-yarleque/spring-boot-hello-world-jenkins-ci.git'
            }
        }
        stage('Building jar file') {
            steps {
                script {
                    sh './gradlew clean build'
                }
            }
        }
        stage('Creating docker image') {
            steps {
                script {
                    challengeImage = docker.build registry + ":latest"
                }
            }
        }
        stage('Pushing image to dockerhub') {
            steps {
                script {
                    docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
                        challengeImage.push()
                    }
                }
            }
        }
    }
}