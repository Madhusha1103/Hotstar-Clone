pipeline {
    agent {
        node {
            label 'AGENT1'
        }
    }

    environment {
        APP_NAME = "scutiarts"
        NODE_ENV = "production"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install --production'
            }
        }

        stage('Run with PM2') {
            steps {
                sh '''
                pm2 describe scutiarts > /dev/null 2>&1 && pm2 delete scutiarts || true
                pm2 start server.js --name scutiarts --update-env
                pm2 save
                pm2 status
                '''
            }
        }
    }
}


