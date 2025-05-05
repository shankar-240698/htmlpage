pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'htmlpage', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    git branch: 'main', url: 'https://github.com/shankar-240698/htmlpage.git', credentialsId: 'htmlpage'
                }
            }
        }
        stage('Deploy to Apache') {
            steps {
                sh 'cp -r * /var/www/html/'  // Make sure the appropriate directory is targeted for your deployment
            }
        }
    }
}
