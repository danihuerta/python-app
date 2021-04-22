pipeline {
    environment {
        registry = '971213/jenkins_training'
        registryCredential = 'dockerhub'
        dockerImage = ''
    }

    agent any

    stages {
        stage('Building image'){
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Deploy image'){
            steps{
                script{
                    dodker.withRegistry('',registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Remove Unused docker image'){
            steps{
                sh 'docker rmi $registry:$BUILD_NUMBER'
            }
        }

    }
}