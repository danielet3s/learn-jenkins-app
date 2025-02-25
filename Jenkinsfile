pipeline {
    agent any
    stages {
        stage('Hello') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                echo "check versions..."
                npm --version
                node --version

                echo "Dependencies..."
                npm ci

                echo "Compiling..."
                npm run build
                '''
            }
        }
        stage('Test') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    echo "running Tests..."
                    npm test
                '''
        }
    }
}
