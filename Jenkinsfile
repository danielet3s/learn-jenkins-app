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
                /*
                    check dependencies
                    Build

                */
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
                    test build/index.html
                    npm test
                '''
            }
        }
        parallel{
            stage('p1'){
                steps{
                    echo "P1"
                }
            }
            stage('p2'){
                steps{
                    echo "P2"
                }
            }
            stage('p3'){
                steps{
                    echo "P3"
                }
            }
        }
    }
    post{
        success{
            // get the report
            junit 'test-results/junit.xml'
        }
    }
}
