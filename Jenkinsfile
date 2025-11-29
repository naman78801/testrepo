pipeline {
    agent any

    stages {
        stage('Deploy Frontend to EC2') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@98.91.23.24 "
                    cd /home/ubuntu/space-science/upload &&
                    git pull origin main &&
                    npm install &&
                    npm run build &&
                    sudo rm -rf /var/www/dev-frontend/* &&
                    sudo cp -r build/* /var/www/dev-frontend/ &&
                    sudo systemctl restart nginx
                "
                '''
            }
        }
    }
}
