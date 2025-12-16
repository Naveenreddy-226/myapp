pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Explicitly specify the branch and credentials
                git branch: 'main',
                    url: 'https://github.com/Naveenreddy-226/myapp'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('myapp:latest')
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'No tests for this simple example, but you can add pytest or unit tests here'
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image('myapp:latest').run('-p 5000:5000')
                }
            }
        }
    }
}
