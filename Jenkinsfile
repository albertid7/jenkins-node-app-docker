pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Use Docker to run npm install with Node.js
                    docker.image('node:18-alpine').inside('-v /var/run/docker.sock:/var/run/docker.sock') {
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def image = docker.build('my-node-app')
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image('my-node-app').run('-d -p 3000:3000 --name my-node-app-container')
                }
            }
        }
    }
    
    post {
        always {
            script {
                // Clean up any existing container with the same name
                sh 'docker stop my-node-app-container || true'
                sh 'docker rm my-node-app-container || true'
            }
        }
    }
}
