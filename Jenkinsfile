pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker {
                    imeage 'node:18-alpine'
                    reusenode-true
                }
            }
            steps {
                Sh '''
                     ls -la
                     node --version
                     npm --version
                     npm ci
                     npm run build
                     ls-la
                '''     
            }
        }
    }
}
