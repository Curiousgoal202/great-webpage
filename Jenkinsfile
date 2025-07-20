pipeline {
    agent any

    environment {
        SLACK_WEBHOOK = credentials('slack_webhook11111')  // Use the ID from Jenkins credentials
    }

    stages {
        stage('Example') {
            steps {
                echo 'Running build stage...'
            }
        }
    }

    post {
        success {
            sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{"text":"✅ Jenkins build succeeded!"}' \
                "$SLACK_WEBHOOK"
            """
        }
        failure {
            sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{"text":"❌ Jenkins build failed!"}' \
                "$SLACK_WEBHOOK"
            """
        }
    }
}
