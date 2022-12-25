pipeline {
    agent  {
                  docker { image 'node:16.13.1-alpine' }
              }
    stages {
        stage('Create Package') {
            steps {
                bat 'mvn package'
            }
        }
    }
}