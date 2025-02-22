pipeline {
    agent any

        // This a list of stages that will be executed in the pipeline 
    stages {
        // the build pipeline stage 
        stage('Build') {
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
        // the test pipeline stage
        stage('Test') {
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
    }

// This is the post section that will be executed after the stages are executed
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
