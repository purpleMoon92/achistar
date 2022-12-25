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
                    sh 'docker build -t kinnari92/achistarimage .'
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
    }
}
