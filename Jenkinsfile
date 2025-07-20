pipeline {
    agent any

    environment {
        SLACK_WEBHOOK = credentials('slack_webhook11111')
    }

    triggers {
        cron('* * * * *')  // ✅ Always run every minute
    }

    stages {
        stage('Build') {
            steps {
                echo "Running scheduled build every minute..."
                // your build logic
            }
        }
    }

    post {
        success {
            script {
                def msg = """
                {
                  "text": "✅ Success: ${env.JOB_NAME} #${env.BUILD_NUMBER} - ${env.BUILD_URL}"
                }
                """
                sh """curl -X POST -H 'Content-type: application/json' --data '${msg}' "${SLACK_WEBHOOK}" """
            }
        }
        failure {
            script {
                def msg = """
                {
                  "text": "❌ Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER} - ${env.BUILD_URL}"
                }
                """
                sh """curl -X POST -H 'Content-type: application/json' --data '${msg}' "${SLACK_WEBHOOK}" """
            }
        }
    }
}
