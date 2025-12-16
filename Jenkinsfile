pipeline {
    agent {
        docker {
            image 'docker:24-dind'           // Docker-in-Docker image
            args '--privileged'              // Needed for DinD to run properly
        }
    }

    environment {
        DOCKER_HOST = 'tcp://localhost:2375'  // Communicate with DinD daemon
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from main branch using GitHub PAT
                git branch: 'main',
                    url: 'https://github.com/Naveenreddy-226/myapp',
                    credentialsId: 'github-pat'
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
                    // Stop any previously running container to avoid port conflicts
                    sh '''
                    docker ps -q --filter "name=myapp-container" | grep -q . && docker stop myapp-container || true
                    docker rm -f myapp-container || true
                    docker run -d --name myapp-container -p 5000:5000 myapp:latest
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo 'Pipeline failed!'
        }
        success {
            echo 'Pipeline succeeded!'
        }
    }
}
