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
        stage('Build and Deploy Image') {
            steps {
                script {
					def imageName = "${registry}"
					docker.withRegistry("https://${registry}", registryCredential) {
						def customImage = docker.build(imageName)
						customImage.push("${BUILD_NUMBER}")
						customImage.push("latest")
					}
                }
            }
        }
        stage('Remove docker images') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
                sh "docker rmi $registry:latest"
            }
        }

    }
}
