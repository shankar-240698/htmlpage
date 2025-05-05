pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/html-site.git'
            }
        }

        stage('Deploy to Apache') {
            steps {
                echo 'Copying files to Apache directory...'
                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r * /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo 'HTML site deployed successfully!'
        }
    }
}
