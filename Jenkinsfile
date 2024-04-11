pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_CREDENTIALS = 'docker-cred'
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/cartservice']], userRemoteConfigs: [[url: 'https://github.com/Chakri2431/Microservice.git']]])
            }
        }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry([credentialsId: env.DOCKER_CREDENTIALS]) {
                        dir('src') {
                            // Build Docker image and tag it
                            sh "docker build -t chakri2431/microservice:my-cartservice ."
                        }
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry([credentialsId: env.DOCKER_CREDENTIALS]) {
                        // Push Docker image to registry
                        sh "docker push chakri2431/microservice:my-cartservice"
                    }
                }
            }
        }
    }
}
