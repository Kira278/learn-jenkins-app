pipeline {
    agent any

    stages {
        stage('Hello1') {
            steps {
              sh  '''
              echo "without docker" 
              ls -la
              touch no_container.txt
              '''
            }
        }
        
        stage('Hello2') {
            agent {
               docker {
                    image 'node:18-alpine'
                    reuseNode true
               }
            }
            steps {
              sh '''
                  echo "with docker"
                  npm --version
                  ls -la
                  touch no_container1.txt
                 '''
            }
        }
    }
}