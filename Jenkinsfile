pipeline {
    agent {
        node {
            label 'AGENT1'
        }
    }

    environment {
        APP_NAME = "Hotstar1"
        NODE_ENV = "production"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Run with PM2') {
            steps {
                sh '''
                pm2 describe $APP_NAME > /dev/null 2>&1 && pm2 delete $APP_NAME || true
                npm install -g serve
                pm2 start serve --name $APP_NAME -- -s build -l 3000
                pm2 save
                pm2 status
                '''
            }
        }
    }
}


