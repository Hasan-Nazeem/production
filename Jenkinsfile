pipeline {

    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: https://github.com/Hasan-Nazeem/production.git
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
