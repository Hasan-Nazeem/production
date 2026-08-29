pipeline {

    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'YOUR-NEW-PRODUCTION-REPO-URL'
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
