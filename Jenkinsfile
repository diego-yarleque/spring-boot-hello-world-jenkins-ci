pipeline {
    environment {
        registry = "dryloayza/codechallenge"
        registryCredential = 'dockerhub'
    }
    agent {
        docker {
            image 'dryloayza/agent:latest'
            registryCredentialsId 'dockerhub'
            registryUrl 'https://hub.docker.com/repository/docker/dryloayza/agent'
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
                    challengeImage = docker.build "dryloayza/codechallenge:latest"
                }
            }
        }
        stage('Pushing image to dockerhub') {
            steps {
                script {
                    docker {
                        registryCredentialsId 'dockerhub'
                        registryUrl 'https://registry.hub.docker.com'
                        challengeImage.push()
                    }
                }
            }
        }
    }
}