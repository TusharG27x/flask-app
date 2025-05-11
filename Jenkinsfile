pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "flask-app-image"
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Checkout the code from the repository
                git 'https://github.com/your-username/flask-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    // Run the Flask app (or unit tests if you have them)
                    sh 'docker run -d -p 5000:5000 $DOCKER_IMAGE'
                    sleep 10  // Allow the app to start
                    sh 'curl http://localhost:5000'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    // You can deploy to a production environment, for example
                    // using Docker, Kubernetes, or AWS (adjust accordingly)
                    echo 'Deploying to production...'
                }
            }
        }
    }

    post {
        always {
            // Clean up
            echo 'Cleaning up...'
            sh 'docker stop $(docker ps -aq) || true'
            sh 'docker rm $(docker ps -aq) || true'
        }
    }
}
