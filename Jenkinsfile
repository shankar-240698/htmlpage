pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/shankar-240698/htmlpage.git'
            }
        }

        stage('Deploy to Apache') {
            steps {
                sshagent(['ssh-key-jenkins']) {
                    sh '''
                        # Ensure remote host is in known_hosts to avoid verification prompt
                        ssh-keyscan -H 18.212.11.83 >> ~/.ssh/known_hosts

                        # Copy files to the remote Apache server
                        scp -o StrictHostKeyChecking=no -r Jenkinsfile about.html css index.html ubuntu@18.212.11.83:/var/www/html/
                    '''
                }
            }
        }
    }
}
