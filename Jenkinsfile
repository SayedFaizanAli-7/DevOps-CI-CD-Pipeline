pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'YOUR_GITHUB_REPOSITORY_URL'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-portfolio:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop devops-portfolio || true
                docker rm devops-portfolio || true

                docker run -d \
                    --name devops-portfolio \
                    -p 8080:80 \
                    devops-portfolio:latest
                '''
            }
        }

    }

    post {

        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed.'
        }

    }
}
