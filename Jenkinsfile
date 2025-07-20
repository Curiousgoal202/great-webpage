pipeline {
    agent any

    environment {
        SLACK_WEBHOOK = credentials('slack_webhook11111')  // Jenkins secret text
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
                def message = """
                {
                  "attachments": [
                    {
                      "fallback": "✅ Build #${env.BUILD_NUMBER} Succeeded!",
                      "color": "#36a64f",
                      "pretext": "*🎉 Build Success Notification 🎉*",
                      "title": "✅ Jenkins Pipeline",
                      "text": "🟢 Build *#${env.BUILD_NUMBER}* for job *${env.JOB_NAME}* completed successfully.",
                      "fields": [
                        {
                          "title": "Status",
                          "value": "Success ✅",
                          "short": true
                        },
                        {
                          "title": "Build Number",
                          "value": "${env.BUILD_NUMBER}",
                          "short": true
                        }
                      ],
                      "footer": "Jenkins CI/CD",
                      "ts": ${System.currentTimeMillis() / 1000}
                    }
                  ]
                }
                """
                sh """curl -X POST -H 'Content-type: application/json' --data '${message}' "$SLACK_WEBHOOK" """
            }
        }

        failure {
            script {
                def message = """
                {
                  "attachments": [
                    {
                      "fallback": "❌ Build #${env.BUILD_NUMBER} Failed!",
                      "color": "#ff0000",
                      "pretext": "*🚨 Build Failure Alert 🚨*",
                      "title": "❌ Jenkins Pipeline",
                      "text": "🔴 Build *#${env.BUILD_NUMBER}* for job *${env.JOB_NAME}* has failed.",
                      "fields": [
                        {
                          "title": "Status",
                          "value": "Failed ❌",
                          "short": true
                        },
                        {
                          "title": "Build Number",
                          "value": "${env.BUILD_NUMBER}",
                          "short": true
                        }
                      ],
                      "footer": "Jenkins CI/CD",
                      "ts": ${System.currentTimeMillis() / 1000}
                    }
                  ]
                }
                """
                sh """curl -X POST -H 'Content-type: application/json' --data '${message}' "$SLACK_WEBHOOK" """
            }
        }
    }
}
