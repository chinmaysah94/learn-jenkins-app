pipeline {
    agent any

    stages {
        //this is a comment
        stage('build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                     ls -la
                     node --version
                     npm --version
                     npm ci
                     npm run build
                     ls -la
                  '''     
            }
        }

       stage('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

          steps {
            sh '''
              test -f build/index.html
              npm test
              
            '''
          }

       }

           stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.52.0-noble'
                    reuseNode true
                }
            }

          steps {
            sh '''
              npm install -g serve
              serve -s build
              npx playwright test
            '''
          }

       }
    }

    post{
        always {
            junit 'test-results/junit.xml'

        }
        }
}
