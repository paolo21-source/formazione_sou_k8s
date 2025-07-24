pipeline {
    agent any
    environment {
        registry = 'paolodocker21/jenkinstest'         
        registryCredential = 'dockerhub'              
        dockerImage = ''
    }

    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/paolo21-source/formazione_sou_k8s']]
                ])
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("${registry}")
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
