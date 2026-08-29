pipeline {

    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker compose down
                    docker compose up -d --build --force-recreate
                    docker image prune -f
                '''
            }
        }
    }
}
