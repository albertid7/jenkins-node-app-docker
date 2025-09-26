pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/my-node-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('my-node-app')
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image('my-node-app').run('-d -p 3000:3000')
                }
            }
        }
    }
}
