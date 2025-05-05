pipeline {
    agent any

    environment {
        REMOTE_HOST = "18.212.11.83"  // Replace with your Ubuntu instance IP
        REMOTE_USER = "ubuntu"            // Replace with your SSH username
        SSH_KEY = credentials('htmlpage-key') // Use Jenkins SSH key credential ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main' 'https://github.com/shankar-240698/htmlpage.git'  // Replace with your GitHub repo
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    sshagent([SSH_KEY]) {
                        sh """
                        scp -r * ${REMOTE_USER}@${REMOTE_HOST}:/var/www/html/
                        """
                    }
                }
            }
        }
    }
}
