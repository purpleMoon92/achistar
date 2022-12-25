pipeline {
    agent  any
    tools{
        maven 'M2_HOME'
    }
    stages {
        stage('Maven Build Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Create Docker Image'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockeruser', variable: 'dockeruser')]) {
                        sh 'docker build -t ${dockeruser}/achistarimage .'
                    }                    
                }
            }
        }
        stage('Host the Docker Image to DockerHub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockeruser', variable: 'dockeruser'), string(credentialsId: 'dockerpwd', variable: 'dockerpwd')]) {
                        sh 'docker login -u ${dockeruser} -p ${dockerpwd}'
                        sh 'docker push ${dockeruser}/achistarimage'
                    }
                }
            }
        }
        stage('Run Docker container using Image from DockerHub '){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockeruser', variable: 'dockeruser'), string(credentialsId: 'dockerpwd', variable: 'dockerpwd')]) {
                        sh 'docker login -u ${dockeruser} -p ${dockerpwd}'
                        sh 'docker pull ${dockeruser}/achistarimage:latest'
                        sh 'docker run -it --name c01 ${dockeruser}/achistarimage /bin/bash'
                    }
                }
            }
        }
    }
}
