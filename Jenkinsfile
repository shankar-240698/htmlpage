pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = credentials('htmlpage') // Use the credentials ID created in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Use the credentials to authenticate with GitHub
                git url: 'https://github.com/shankar-240698/htmlpage.git', credentialsId: 'github-credentials'
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
