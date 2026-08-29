pipeline {

    agent any

    stages {

        stage('Checkout Code') {
            steps {
                dir('/home/ubuntu/production') {
                    sh '''
                        git fetch origin
                        git reset --hard origin/main
                    '''
                }
            }
        }

        stage('Deploy Application') {
            steps {
                dir('/home/ubuntu/production') {
                    sh '''
                        docker compose down
                        docker compose up -d --build --force-recreate
                        docker image prune -f
                    '''
                }
            }
        }
    }
}
