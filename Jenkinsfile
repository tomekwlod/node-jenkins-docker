pipeline {
    environment {
        registry = "twlphaseii/node-jenkins-docker"
        registryCredential = 'dockerhub'
    }

    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:8.12.0-alpine'
                }
            }
            steps {
                sh 'npm install' 
            }
        }

        stage('Test') {
			agent {
                docker {
                    image 'node:8.12.0-alpine'
                }
            }
            steps {
                sh 'npm test'
            }
        }
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }

    }
}
