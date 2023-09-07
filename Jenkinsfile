pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = '192.168.200.12:5000'
        IMAGE_NAME = 'hi-world'
        TAG = 'latest'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("${DOCKER_REGISTRY}/${IMAGE_NAME}:${TAG}", "-f Dockerfile .")
                }
            }
        }
        
        stage('Push to Registry') {
            steps {
                
                script {
                    def dockerImage = docker.image("${DOCKER_REGISTRY}/${IMAGE_NAME}:${TAG}")
                    docker.withRegistry('http://192.168.200.12:5000') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
