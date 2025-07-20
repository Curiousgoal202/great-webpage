pipeline {
    agent any

    stages {
        stage('Example') {
            steps {
                echo 'Running build stage...'
            }
        }
    }

    post {
        success {
            sh '''
            curl -X POST -H 'Content-type: application/json' \
            --data '{"text":"✅ Jenkins build succeeded!"}' \
            https://hooks.slack.com/services/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
            '''
        }
        failure {
            sh '''
            curl -X POST -H 'Content-type: application/json' \
            --data '{"text":"❌ Jenkins build failed!"}' \
            https://hooks.slack.com/services/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
            '''
        }
    }
}
