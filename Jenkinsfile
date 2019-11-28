pipeline {
    environment {
        registry = "twlphaseii/simple-node-app"
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
            steps {
                sh 'ls -alh'
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



// node {
    
	

//     env.AWS_ECR_LOGIN=true
//     def newApp
//     def registry = 'gustavoapolinario/microservices-node-todo-frontend'
//     def registryCredential = 'dockerhub'
	
// 	stage('Build') {
// 		sh 'npm install'
// 	}
// 	stage('Test') {
// 		sh 'npm test'
// 	}
// 	stage('Building image') {
//         docker.withRegistry( 'https://' + registry, registryCredential ) {
// 		    def buildName = registry + ":$BUILD_NUMBER"
// 			newApp = docker.build buildName
// 			newApp.push()
//         }
// 	}
// 	stage('Registring image') {
//         docker.withRegistry( 'https://' + registry, registryCredential ) {
//     		newApp.push 'latest2'
//         }
// 	}
//     stage('Removing image') {
//         sh "docker rmi $registry:$BUILD_NUMBER"
//         sh "docker rmi $registry:latest"
//     }
    
// }
