pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ECR_REGISTRY = '239155901548.dkr.ecr.ap-south-1.amazonaws.com'
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Images') {
            steps {
                sh '''
                    docker build -t frontend:${IMAGE_TAG} ./client
                    docker build -t backend:${IMAGE_TAG} ./server
                '''
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                    aws ecr get-login-password --region ${AWS_REGION} | \
                    docker login --username AWS --password-stdin ${ECR_REGISTRY}
                '''
            }
        }

        stage('Tag & Push Images') {
            steps {
                sh '''
                    docker tag frontend:${IMAGE_TAG} ${ECR_REGISTRY}/frontend:${IMAGE_TAG}
                    docker tag backend:${IMAGE_TAG} ${ECR_REGISTRY}/backend:${IMAGE_TAG}

                    docker push ${ECR_REGISTRY}/frontend:${IMAGE_TAG}
                    docker push ${ECR_REGISTRY}/backend:${IMAGE_TAG}
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker compose down

                    docker compose pull

                    IMAGE_TAG=${IMAGE_TAG} docker compose up -d --force-recreate

                    docker image prune -f
                '''
            }
        }
    }
}
