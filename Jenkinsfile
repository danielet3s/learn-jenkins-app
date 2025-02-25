pipeline {
    agent any

    stages {
        stage('Hello') {
            agent {
                docker{
                    image 'node:18-alpine'
                }
            }
            steps {
                echo 'Hello World'
                sh 'npm --version'
            }
        }
    }
}
