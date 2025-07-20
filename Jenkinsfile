pipeline {
    agent any

    environment {
        SLACK_WEBHOOK = credentials('slack_webhook11111')  // Jenkins credential ID
    }

    triggers {
        // 🔁 Run job every 1 minute (regardless of code change)
        cron('* * * * *')

        // 🔁 Also poll Git repo for changes (works only if a Git repo is configured)
        pollSCM('* * * * *')  // Every minute
    }

    stages {
        stage('Build') {
            steps {
                echo "🔧 Building the project..."
                // Place your actual build commands here (like mvn build, npm run, etc.)
            }
        }
    }

    post {
        success {
            script {
                def message = """
                {
                  "text": "*🎉 Build Success!*\n\n*Job:* ${env.JOB_NAME}\n*Build #:* ${env.BUILD_NUMBER}\n🔗 <${env.BUILD_URL}|Click to View Build>\n*Status:* ✅ Passed"
                }
                """
                sh """
                    curl -X POST -H 'Content-type: application/json' \
                    --data '${message}' \
                    "${SLACK_WEBHOOK}"
                """
            }
        }

        failure {
            script {
                def message = """
                {
                  "text": "*🚨 Build Failed!*\n\n*Job:* ${env.JOB_NAME}\n*Build #:* ${env.BUILD_NUMBER}\n🔗 <${env.BUILD_URL}|Click to View Build>\n*Status:* ❌ Failed"
                }
                """
                sh """
                    curl -X POST -H 'Content-type: application/json' \
                    --data '${message}' \
                    "${SLACK_WEBHOOK}"
                """
            }
        }
    }
}
