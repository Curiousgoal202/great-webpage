pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Curiousgoal202/great-webpage.git'
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo cp index.html /var/www/html/index.html'
            }
        }
    }
    post {
        success {
            slackSend (color: '#00FF00', message: "✅ SUCCESS: Job '${env.JOB_NAME} #${env.BUILD_NUMBER}' deployed the page!")
        }
        failure {
            slackSend (color: '#FF0000', message: "❌ FAILED: Job '${env.JOB_NAME} #${env.BUILD_NUMBER}' failed.")
        }
    }
}
