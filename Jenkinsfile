pipeline {
    agent any

    environment {
        SLACK_WEBHOOK = credentials('slack_webhook11111')  // Jenkins credentials ID
    }

    triggers {
        pollSCM('* * * * *') // Runs every 1 minute
    }

    stages {
        stage('Build') {
            steps {
                echo "👷‍♂️ Building the project..."
                // Your build logic here
            }
        }
    }

    post {
        success {
            script {
                def msg = """
                {
                    "attachments": [
                        {
                            "color": "good",
                            "pretext": ":tada: *Build Successful!*",
                            "title": "✅ Job: ${env.JOB_NAME}",
                            "fields": [
                                {
                                    "title": "Build Number",
                                    "value": "${env.BUILD_NUMBER}",
                                    "short": true
                                },
                                {
                                    "title": "Status",
                                    "value": "SUCCESS",
                                    "short": true
                                },
                                {
                                    "title": "Build URL",
                                    "value": "${env.BUILD_URL}"
                                }
                            ]
                        }
                    ]
                }
                """
                sh """
                    curl -X POST -H 'Content-type: application/json' \
                    --data '${msg.replaceAll("'", "'\\''")}' \
                    "${SLACK_WEBHOOK}"
                """
            }
        }

        failure {
            script {
                def msg = """
                {
                    "attachments": [
                        {
                            "color": "danger",
                            "pretext": ":x: *Build Failed!*",
                            "title": "❌ Job: ${env.JOB_NAME}",
                            "fields": [
                                {
                                    "title": "Build Number",
                                    "value": "${env.BUILD_NUMBER}",
                                    "short": true
                                },
                                {
                                    "title": "Status",
                                    "value": "FAILURE",
                                    "short": true
                                },
                                {
                                    "title": "Build URL",
                                    "value": "${env.BUILD_URL}"
                                }
                            ]
                        }
                    ]
                }
                """
                sh """
                    curl -X POST -H 'Content-type: application/json' \
                    --data '${msg.replaceAll("'", "'\\''")}' \
                    "${SLACK_WEBHOOK}"
                """
            }
        }
    }
}
