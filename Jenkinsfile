pipeline {
    agent any

    environment {
        SLACK_WEBHOOK = credentials('slack_webhook11111')  // Replace with your credential ID
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
            script {
                sh """
                    curl -X POST -H 'Content-type: application/json' \\
                    --data '{
                        "attachments": [
                            {
                                "fallback": "✅ Jenkins Build Succeeded!",
                                "color": "good",
                                "pretext": "*🎉 Build Notification - SUCCESS 🎉*",
                                "title": "${env.JOB_NAME} - #${env.BUILD_NUMBER}",
                                "title_link": "${env.BUILD_URL}",
                                "text": "✅ *Build succeeded!*",
                                "fields": [
                                    {
                                        "title": "Job",
                                        "value": "${env.JOB_NAME}",
                                        "short": true
                                    },
                                    {
                                        "title": "Build Number",
                                        "value": "#${env.BUILD_NUMBER}",
                                        "short": true
                                    }
                                ],
                                "footer": "Jenkins CI/CD 💻",
                                "ts": $(date +%s)
                            }
                        ]
                    }' "$SLACK_WEBHOOK"
                """
            }
        }

        failure {
            script {
                sh """
                    curl -X POST -H 'Content-type: application/json' \\
                    --data '{
                        "attachments": [
                            {
                                "fallback": "❌ Jenkins Build Failed!",
                                "color": "danger",
                                "pretext": "*💥 Build Notification - FAILURE 💥*",
                                "title": "${env.JOB_NAME} - #${env.BUILD_NUMBER}",
                                "title_link": "${env.BUILD_URL}",
                                "text": "❌ *Build failed!*",
                                "fields": [
                                    {
                                        "title": "Job",
                                        "value": "${env.JOB_NAME}",
                                        "short": true
                                    },
                                    {
                                        "title": "Build Number",
                                        "value": "#${env.BUILD_NUMBER}",
                                        "short": true
                                    }
                                ],
                                "footer": "Jenkins CI/CD 💻",
                                "ts": $(date +%s)
                            }
                        ]
                    }' "$SLACK_WEBHOOK"
                """
            }
        }
    }
}

