pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // your build steps here
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
