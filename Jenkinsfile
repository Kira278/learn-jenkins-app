pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '3016f48d-e387-4382-823e-0e30e21da3c7'
        NETLIFY_AUTH_TOKEN = credentials ('netlify-token')
    }

    stages {
        
        stage('Build') {
            agent {
                docker { image 'node:18-alpine'
                         reuseNode true
                         }
            }
/*ls -la*/

            steps {
                
                sh '''
                
                node --version
                npm --version
                npm ci
                npm run build
                
                '''
            }
        }
        stage('Tests')
        {
            agent {
            docker { image 'node:18-alpine'
                         reuseNode true
                         }
            }
            steps{
                sh '''
                test -f build/index.html
                npm test
                '''
            }
                  
        }

            
        
       
       stage('Deploy')
       {
        agent {
                docker { image 'node:18-alpine'
                         reuseNode true
                         }
       }
    steps 
    {
        sh'''
        npm install netlify-cli
        node_modules/.bin/netlify --version
        echo "Deploying to production, Site id: $NETLIFY_SITE_ID"
        node_modules/.bin/netlify status 
        node_modules/.bin/netlify deploy --dir=build --prod
        
        
        '''
    }
/*node_modules/.bin/netlify deploy --dir=build --prod*/
       }
    }
        
        

    
    /*stage('E2E')
        {
            agent {
            docker { image 'mcr.microsoft.com/playwright:v1.57.0-noble'
                         reuseNode true

                         }
            }
            steps{
                sh '''
                npm install serve
                node_modules/.bin/serve -s build &
                sleep 10
                npx playwright test --reporter=html
                '''
            }
        }*/

    
    
   post {
        always {
            junit 'jest-results/junit.xml'
        }
    }

}