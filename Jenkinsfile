
pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_CREDENTIALS = 'docker-cred'
        
    }

    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }

        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/cartservice']], userRemoteConfigs: [[url: 'https://github.com/Chakri2431/Microservice.git']]])
            }
        }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    dir('*/cartservice/src'){
                        
                    }
                    withDockerRegistry(credentialsId: env.DOCKER_CREDENTIALS, toolName: 'docker') {
                        
                        sh "docker build -t chakri2431/microservice:my-cartservice ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                     dir('*/cartservice/src'){
                        
                    }
                    withDockerRegistry(credentialsId: env.DOCKER_CREDENTIALS, toolName: 'docker') {
                        sh "docker push chakri2431/microservice:my-cartservice"
                    }
                }
            }
        }
    }
}
