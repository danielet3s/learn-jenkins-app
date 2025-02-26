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
                npm install serve
                node_modules/.bin/serve -s build 
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
        stage('parallel'){
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
        stage('Deploy'){
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{

                // for this test we will deploy in netlify 
                // see netlify https://docs.netlify.com/cli/get-started/#app
                sh '''
                    chown -R $(whoami) /usr/local/lib/node_modules
                    npm install netlify-cli -g
                    node_modules/.bin/netflify --version



                '''
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
