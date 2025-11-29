pipeline {
    agent any

    stages {

        stage('Deploy Frontend to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@98.91.23.24 "
                        cd /home/ubuntu/space-science/upload &&
                        echo '--- Pulling latest code ---' &&
                        git pull origin main &&
                        
                        echo '--- Installing dependencies ---' &&
                        npm install &&
                        
                        echo '--- Building frontend ---' &&
                        npm run build &&
                        
                        echo '--- Copying build to Nginx directory ---' &&
                        sudo rm -rf /var/www/dev-frontend/* &&
                        sudo cp -r build/* /var/www/dev-frontend/ &&
                        
                        echo '--- Restarting Nginx ---' &&
                        sudo systemctl restart nginx
                    "
                    '''
                }
            }
        }
    }
}
