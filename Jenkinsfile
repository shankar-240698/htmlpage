pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/shankar-240698/htmlpage.git'
            }
        }

        stage('Deploy to Apache') {
            environment {
                REMOTE_HOST = '18.212.11.83'
                REMOTE_USER = 'ubuntu'
                REMOTE_TEMP = '/home/ubuntu/deploy'
                REMOTE_HTML = '/var/www/html'
            }

            steps {
                sshagent(credentials: ['ubuntu']) {
                    sh '''
                        # Ensure .ssh directory exists and host is known
                        mkdir -p ~/.ssh
                        ssh-keyscan -H $REMOTE_HOST >> ~/.ssh/known_hosts

                        # Create remote temp directory
                        ssh $REMOTE_USER@$REMOTE_HOST "mkdir -p $REMOTE_TEMP"

                        # Copy files to remote temp directory
                        scp -o StrictHostKeyChecking=no -r Jenkinsfile about.html css index.html $REMOTE_USER@$REMOTE_HOST:$REMOTE_TEMP/

                        # Move files from temp to Apache web root using sudo
                        ssh $REMOTE_USER@$REMOTE_HOST "sudo mv $REMOTE_TEMP/* $REMOTE_HTML/"
                    '''
                }
            }
        }
    }
}
