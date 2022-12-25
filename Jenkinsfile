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
                    withCredentials([string(credentialsId: 'dockerHubUsername', variable: 'dockerhubuser')]) {
                        sh 'docker build -t ${dockerhubuser}/achistarimage .'
                    }
                }
            }
        }
    }
}
