pipeline {

    agent any

    stages {

        stage('Checkout Code') {
            steps {
                sh '''
                    cd /home/ubuntu/production
                    git fetch origin
                    git reset --hard origin/main
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    cd /home/ubuntu/production

                    docker compose down

                    docker compose up -d --build --force-recreate

                    docker image prune -f
                '''
            }
        }
    }
}

