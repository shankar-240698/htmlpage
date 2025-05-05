pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/shankar-240698/htmlpage.git'
            }
        }

        stage('Deploy to Apache') {
            steps {
                sshagent(['ssh-key-jenkins']) {
                    sh '''
                        mkdir -p ~/.ssh
                        ssh-keyscan -H 18.212.11.83 >> ~/.ssh/known_hosts
                        scp -o StrictHostKeyChecking=no -r Jenkinsfile about.html css index.html ubuntu@18.212.11.83:/var/www/html/
                    '''
                }
            }
        }
    }
}
